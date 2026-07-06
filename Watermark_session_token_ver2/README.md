# Watermark Session Token Issuance ver2

## 1. Overview

This project was designed to resolve bottlenecks in token issuance that occurred during real-time watermark session generation.  
By improving the synchronous RDB-based architecture and applying a serverless design with a non-linear index-based algorithm,  
we achieved the following:

- **30% peak-latency reduction** in token issuance
- **5M+ race-free tokens** issued across three regions (Seoul, Oregon, Frankfurt)
- 100% duplication-free token generation without DB uniqueness checks
- High scalability

---

## 2. Problem

- Bottlenecks occurred under high concurrent token issuance requests
- TPS (transactions per second) limit due to synchronous RDB structure
- Locks or duplication checks required, resulting in increased latency

---

## 3. Solution

- Pre-generated token queue in Redis for instant response without DB access
- AWS Lambda asynchronously creates and stores tokens
- Introduced a collision-free token generation algorithm
- CloudWatch and SNS monitor Redis memory usage and trigger automatic token refill

---

## 4. Architecture

### Token Issuance Flow

1. User sends a token request via API
2. Redis returns a pre-issued token immediately
3. SQS message triggers Lambda
4. Lambda stores issued token information into the RDB

```mermaid
sequenceDiagram
    autonumber
    participant C as Client
    participant R as Redis<br/>(pre-issued token queue)
    participant Q as Amazon SQS
    participant L as AWS Lambda
    participant DB as RDB

    C->>R: Token request via API
    R-->>C: Pre-issued token returned immediately (no DB access)
    C->>Q: Publish issued-token info
    Q->>L: Trigger Lambda
    L->>DB: Persist issued-token record (async)
```

---

### Token Generation Flow

1. When Redis memory falls below 200MB, CloudWatch alarm is triggered
2. SNS topic invokes a single Lambda function
3. Lambda generates new tokens and stores them in Redis

```mermaid
sequenceDiagram
    autonumber
    participant R as Redis
    participant CW as CloudWatch
    participant S as SNS Topic
    participant L as AWS Lambda

    CW->>CW: Alarm fires when Redis memory < 200MB
    CW->>S: Publish to SNS topic
    S->>L: Invoke a single Lambda function
    L->>L: Generate new tokens (skew transform)
    L->>R: Refill pre-issued token queue
```

---

## 5. Collision-Free Token Generation Algorithm (Skew Transform Based)

### Why This Algorithm?

Previous token generation relied on random strings or UUIDs.  
To ensure uniqueness, a DB check was required, which caused:

- Bottlenecks due to duplication checks in high-concurrency environments
- Decreased TPS due to locks or transactional operations

### Our Approach

We use a Skew Transform, a non-linear mapping based on a sequential index,  
which allows deterministic, unique, and non-repeating token generation.

```python
class PseudoRandomGenerator:
    def __init__(self, a, b):
        self.a = a
        self.b = b
    def skew_transform(self, x):
        return ((self.a ^ x) + (self.b * x)) % (2**56)
    def get_number(self, index):
        if 0 <= index < 2**56:
            return self.skew_transform(index)
```

Each sequential index maps to a unique token deterministically, so tokens are
generated collision-free without any DB lookup or lock on the issuance path.
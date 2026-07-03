# Hi, I'm Seung Bum Jung

## 🔧 The Problem I Solve

Most engineering teams hit a wall when **production reliability** and **HPC/research-grade infrastructure** need to coexist. Web-scale distributed systems engineers don't speak HPC. HPC researchers don't ship production AWS code. Healthcare AI teams need both, and almost no one has both.

## ⚠️ Why It Gets Worse

I've watched the same pattern repeat:
- Legacy systems quietly cap throughput, but nobody redesigns the data path — they tune it
- Research code lives on a laptop until it dies on the cluster
- "We'll add compliance later" becomes "we shipped, now what?"

The cost? 50% over-spending, 30% latency you can't fix with caching, and an LLM you can't actually ship into a regulated environment.

## ✅ What I Bring

I'm the engineer who lives in both worlds.

**Production AWS at scale (4 years at Doverunner):**
- Redesigned a synchronous-RDB watermark token system into a **Lambda + Redis + SNS** architecture → **5M+ race-free tokens** across Seoul, Oregon, Frankfurt with **30% peak-latency reduction**
- Replaced a Hybrik-based encoding SaaS with a self-hosted **AWS EKS** pipeline → **50% cost cut, 30% throughput lift**
- Reduced 100-user video conference room initialization from 0.6s to 0.1s — a **6× user-facing latency improvement** at TmaxWAPL

**HPC + ML research at SLU HPC Lab (M.S. CS, Dec 2026):**
- Federated Learning parallelization on SLURM + NVIDIA L40S with empirical Amdahl analysis
- Gaussian Process Regression + LSTM pipeline for clinical force prediction with uncertainty estimation
- Joining CARLA distributed simulation project, SC2026 workshop submission

**Applied LLM (Summer 2026 →):**
- Funded RA on a HIPAA-compliant clinical LLM chatbot for MCI patient support — iPad frontend, institutional backend, BAA-grounded data architecture

## 📩 What I'm Looking For

Mid-level (SDE II / SWE II) roles in:
- ☁️ Cloud / Distributed Systems Infrastructure (AWS, Datadog, Mastercard, Cloudflare)
- 🤖 ML / AI Platform Engineering (CoreWeave, Anyscale, Modal Labs)
- 🎬 Video / Streaming Infrastructure (AWS Elemental, Akamai, Twitch, Bitmovin)
- 🏥 Healthcare AI (Cigna-Evernorth, Lumeris, Tempus, Hippocratic AI)

📍 St. Louis, MO · Open to relocation (Seattle, Bay Area, NYC, Portland, Boston, Pittsburgh) · F-1 OPT + 3-year STEM extension eligible · Available **January 2027**

→ DM open. Reach me via [LinkedIn](https://www.linkedin.com/in/seungbum-jung-6a105317a/) or email tofoth@gmail.com.

## Research

### ✅ Parallelizing Federated Learning Client Simulation [📄 Read More](https://github.com/back99/fl-simulation)
- **Identified** the single-process bottleneck capping FL research throughput; **prototyped** Python `ProcessPoolExecutor` parallelization and **diagnosed** a PyTorch tensor-pickling deadlock at the IPC boundary, **resolving** it via NumPy serialization
- **Measured ~1.27× stable speedup** across 50–200 Non-IID MNIST clients on an 8-core CPU; **proved** an Amdahl ceiling (~24% parallel fraction), pointing the next iteration to multi-node FL rather than further single-machine tuning
- Future work (Summer 2026 →): scale FL to multi-node SLU Libra HPC, introduce Asynchronous FedAvg, and adopt CIFAR-10 + ResNet-18 workloads  
  **Stack:** Python, PyTorch, NumPy, multiprocessing, MNIST, FedAvg

### ✅ Dental Aligner ML Force Prediction [📄 Read More](https://github.com/back99/dental-ml-force-prediction)
- **GPR for thickness extrapolation**: Found XGBoost collapsed to flat lines outside the training range (0.25/0.5mm), useless for predicting forces (Fx–Fz, Tx–Tz) on U6/U7 molars at unseen thicknesses (0.75/1.0/1.25mm). Re-architected with **Gaussian Process Regression** (Matern kernel) for **μ ± 2σ** uncertainty; augmented training with weighted-delta-method synthetic 0.75mm data to distinguish 1.0 vs 1.25mm predictions
- **LSTM LOO + Partial Observation forecasting**: Reframed as "given a new patient's early measurements, forecast later force/moment trajectory." Designed a **60-experiment matrix** (5 cohorts × 3 horizons × 4 sheets) — train on 4 other cohorts plus target cohort's first (11−k) points, predict the last k ∈ {1,2,3} points
- **Model**: LSTM(128, 2 layers, dropout 0.2) → Dense(64) → scalar, 300 epochs with StepLR
- **Complementary design**: GPR covers **spatial** extrapolation (thickness), LSTM covers **temporal** extrapolation (14-day window). Trained on **NVIDIA L40S** GPUs under **SLURM** on the SLU Libra HPC cluster  
  **Stack:** Python, PyTorch, GPyTorch, XGBoost, scikit-learn, pandas, numpy, SLURM

### 🟣 Clinical LLM Chatbot for MCI Patient Support — **Upcoming (Summer 2026 →)**
- Funded RA project at SLU HPC Lab (advisor: Prof. Ted Ahn). Design and build an **iPad-based conversational AI** intervention for patients with **Mild Cognitive Impairment (MCI)**, deployed in a **HIPAA-compliant** clinical setting as a feasibility pilot supporting a future **NIH R01** application
- End-to-end ownership: iPad kiosk frontend + institutional backend + LLM API integration (OpenAI / Claude). Initial release uses existing APIs with prompt engineering and safety guardrails rather than fine-tuning — prioritizing speed-to-clinic over model novelty
- HIPAA + BAA + privacy-first data architecture: capture only de-identified engagement metadata (topics discussed, session duration, dates, participant ID) — **no raw audio or full conversation transcripts**
- Pilot evaluation (~15 participants, 6 months): feasibility, iPad usability, engagement patterns from metadata, and preliminary effectiveness on depression, anxiety, insomnia, and cognitive function trends  
  **Planned Stack:** Python, OpenAI / Claude APIs, prompt engineering, safety guardrails, iPad (frontend), institutional backend (HIPAA), BAA, de-identified metadata only

## Experience — Doverunner (formerly Inka Entworks) · Software Engineer · 2023.04 – 2025.09

### ✅ Watermark Token Issuance Optimization [📄 Read More](Watermark_session_token_ver2)
> **Redesigned** the legacy synchronous-RDB token service into a non-linear-index Lambda + Redis + SNS event-driven architecture, **to fix** peak-time latency spikes and regional index collisions blocking scale-out, **delivering 30% peak-latency reduction and 5M+ race-free tokens** across Seoul, Oregon, and Frankfurt.

**Stack:** Kotlin, AWS Lambda, Redis, SNS, CloudWatch, RDS

### ✅ Distributed Encoding System on AWS EKS [📄 Read More](Distributed_transcoding)
> **Designed and built** a containerized encoding pipeline on AWS EKS with GOP-aware video partitioning and Redis-based job control with auto-failover, **to replace** a Hybrik-based external SaaS that was cost-prohibitive and inelastic at scale, **cutting encoding cost 50% and lifting throughput 30%**.

**Stack:** Kotlin, Spring Boot, AWS EKS, Docker, Redis, FFmpeg

### ✅ Legacy API Refactoring & Kotlin Migration
> **Led migration** of entangled base64-Java handlers into modular Kotlin codebases under DDD boundaries with Kafka-based event streaming, **to unblock** API safety and testability blocks preventing onboarding and deploys, **improving** test coverage, deployment cadence, and team onboarding by isolating reusable domain logic.

**Stack:** Kotlin, Spring Boot, Kafka, DDD

### ✅ Transcoding & Packaging Module Enhancement
> **Modularized** the encoding pipeline into media-info / error-handling / packaging submodules and added multi-aspect (16:9, 1:1, 9:16) + HD/FHD/UHD quality tiers, **to enable** cross-team reuse, **delivering** shared modules adopted across encoding services.

**Stack:** Kotlin, FFmpeg

---

## Experience — Tmax · Software Engineer / Research Lab · 2021.08 – 2023.04 (1 yr 9 mo, across TmaxWAPL and TmaxOS Research Lab)

### ✅ Video Conference Room Initialization (6× faster)
> **Traced** 100-user video conference room join latency to chat and account initialization being coupled on the join path, **decoupled** those dependencies and **introduced** async task queues to move initialization off the critical path, **reducing per-user setup from 0.6s to 0.1s — a 6× user-facing latency improvement**.

**Stack:** Node.js, Express, MongoDB, Redis

### ✅ CMS Performance Optimization
> **Refactored** Redis caching with TTL-based eviction and **introduced** Redis Pub/Sub for real-time notifications, **to address** cache inefficiency and notification scalability blocks under high concurrency, **lowering** server load and notification latency while modularizing chat / alarm / account services for future scaling.

**Stack:** Java, Spring, Redis (Cache + Pub/Sub), MongoDB

### ✅ Kafka-Based Room Lifecycle Event Server
> **Built** a Kafka-based backend capturing ~80K session lifecycle events end-to-end with a schema designed to support both ad-hoc debugging and downstream metric pipelines, **to address** the lack of room-level observability blocking debugging, analytics, and metric-driven feature work, **unblocking** debugging, analytics, and metric-based feature extensions that were previously impossible.

**Stack:** Java, Kafka, Spring, MongoDB

## Education

- **M.S. in Computer Science (in progress)** — Saint Louis University, USA, Aug 2025 – Dec 2026 (expected)  
  Advisor: Prof. Ted Ahn · Lab: High Performance Computing Lab · GPA: 3.63 / 4.0
- **B.S. in Computer Engineering** — Ajou University, South Korea, 2015–2018

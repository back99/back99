# Hi, I'm Seung Bum Jung

## About Me

Hello! I'm Seung Bum Jung — a software engineer currently pursuing a Master's in Computer Science at Saint Louis University.

My work pattern is consistent: identify the real bottleneck in a legacy system, then redesign it — not just optimize around it. Concrete examples include a 50% encoding cost reduction (Hybrik → AWS EKS), a 30% token-issuance latency reduction (synchronous RDB → Lambda + Redis + SNS), and a 6× faster video-conference room initialization.

I'm expanding that production-engineering depth into AI/ML systems — Federated Learning at HPC scale, Bayesian models on GPUs, and (from Summer 2026) a HIPAA-compliant clinical LLM chatbot for MCI patient support. The goal is to bridge industry-scale system design with applied ML in regulated, real-world settings.

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

## Experience

### ✅ Distributed Encoding System on AWS EKS [📄 Read More](Distributed_transcoding)
- **Found** the Hybrik-based pipeline cost-prohibitive and inelastic at scale
- **Designed** a containerized encoding pipeline on AWS EKS with GOP-aware video partitioning and Redis-based job control with auto-failover, replacing the closed-source vendor stack
- **Cut encoding cost by 50%** and **lifted throughput by 30%**  
  **Stack:** Kotlin, Spring Boot, AWS EKS, Redis, Docker, FFmpeg

### ✅ Watermark Token Issuance Optimization [📄 Read More](Watermark_session_token_ver2)
- **Diagnosed** peak-time latency spikes and regional index collisions in the legacy synchronous-RDB token service
- **Redesigned** the data path as a non-linear index generator on AWS Lambda + Redis with SNS-driven regeneration, removing the global lock and unifying regional indexing into a single WM_INDEX
- **Delivered 30% peak-latency reduction** and provisioned **5M+ tokens** race-free across Seoul / Oregon / Frankfurt  
  **Stack:** Kotlin, Redis, AWS Lambda, CloudWatch, SNS

### ✅ Legacy API Refactoring & Kotlin Migration
- **Identified** that base64-string transport and entangled Java handlers made the API both unsafe and untestable
- **Led** a migration to modular Kotlin codebases under DDD boundaries with a structured handler–resolver protocol
- **Decoupled** synchronous calls behind Kafka event streams; improved test coverage and deployment cadence while preserving wire compatibility  
  **Stack:** Kotlin, Spring Boot, Kafka, DDD

## Education

- **M.S. in Computer Science (in progress)** — Saint Louis University, USA, Aug 2025 – Dec 2026 (expected)  
  Advisor: Prof. Ted Ahn · Lab: High Performance Computing Lab · GPA: 3.63 / 4.0
- **B.S. in Computer Engineering** — Ajou University, South Korea, 2015–2018

# Hi, I'm Seung Bum Jung

## About Me

Hello! I'm Seung Bum Jung — a software engineer currently pursuing a Master's in Computer Science at Saint Louis University.

My work pattern is consistent: identify the real bottleneck in a legacy system, then redesign it — not just optimize around it. Concrete examples include a 50% encoding cost reduction (Hybrik → AWS EKS), a 30% token-issuance latency reduction (synchronous RDB → Lambda + Redis + SNS), and a 6× faster video-conference room initialization.

I'm expanding that production-engineering depth into AI/ML infrastructure — Federated Learning at HPC scale, Bayesian models on GPUs, and (from Summer 2026) a retrieval-augmented LLM project for medical conversational AI. The goal is to bridge industry-scale system design with applied ML research.

## Research

### ✅ Parallelizing Federated Learning Client Simulation [📄 Read More](https://github.com/back99/fl-simulation)
- **Identified** the single-process bottleneck capping FL research throughput; **prototyped** Python `ProcessPoolExecutor` parallelization and **diagnosed** a PyTorch tensor-pickling deadlock at the IPC boundary, **resolving** it via NumPy serialization
- **Measured ~1.27× stable speedup** across 50–200 Non-IID MNIST clients on an 8-core CPU; **proved** an Amdahl ceiling (~24% parallel fraction), pointing the next iteration to multi-node FL rather than further single-machine tuning
- Future work (Summer 2026 →): scale FL to multi-node SLU Libra HPC, introduce Asynchronous FedAvg, and adopt CIFAR-10 + ResNet-18 workloads  
  **Stack:** Python, PyTorch, NumPy, multiprocessing, MNIST, FedAvg

### ✅ Dental Aligner ML Force Prediction [📄 Read More](https://github.com/back99/dental-ml-force-prediction)
- **Found** that XGBoost predictions collapsed to flat lines beyond the training range — useless for predicting orthodontic forces (Fx, Fy, Fz, Tx, Ty, Tz) at unseen aligner thicknesses (0.75/1.0/1.25mm) on U6/U7 molars
- **Re-architected** with **Gaussian Process Regression** (Matern kernel, ν=1.5) for principled μ ± 2σ uncertainty so the "I don't know" regions are visible to clinicians
- **Augmented** training with simulated 0.75mm data via a weighted delta method (w = 0.5~1.5), enabling the model to distinguish 1.0mm vs 1.25mm predictions that had previously collapsed to the same curve
- Also explored **LSTM** with **Leave-One-Out Cross-Validation (5 folds)** to predict patient cohort force/moment time-series (0h–336h) on the same dataset
- **Operationalized** on **NVIDIA L40S (48GB VRAM)** GPUs via GPyTorch, scheduled with **SLURM** on the SLU Libra HPC cluster  
  **Stack:** Python, PyTorch, GPyTorch, XGBoost, scikit-learn, pandas, numpy, matplotlib, seaborn, SLURM

### 🟣 RAG-Based Conversational AI for MCI Patient Support — **Upcoming (Summer 2026 →)**
- Joining as funded RA at SLU HPC Lab. Core design problem: how to keep an LLM's answers **grounded in a curated medical knowledge base** — not free-generated — under the safety bar required for **Mild Cognitive Impairment (MCI)** patient support
- Planned approach: a retrieval-augmented generation (RAG) pipeline (vector retrieval + open-weight LLM) served on the same **SLURM / NVIDIA L40S** HPC workflow I already operate
- Will design domain-appropriate evals (factuality vs. curated sources, refusal behavior on out-of-scope queries, retrieval recall@k) so improvements are measurable  
  **Planned Stack:** Python, PyTorch, Hugging Face, vLLM, FAISS/Chroma, embedding models, SLURM, NVIDIA L40S

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

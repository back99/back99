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

**The rare engineer who bridges production AWS at scale, HPC-based ML/AI research, and regulated healthcare LLM deployment** — three intersecting depths that almost never coexist in one person.

**🏥 Regulated Healthcare LLM (funded RA, Summer 2026 →):**
- HIPAA-compliant clinical LLM chatbot for MCI patient support at SLU HPC Lab — **working prototype complete**: device pairing, onboarding, AI-initiated proactive conversation, coordinator dashboard, **204 Vitest tests**
- Server-side crisis detection (Code Blue escalation, 988 lockout) + prompt-level safety guardrails for a vulnerable population
- BAA-grounded data architecture (engagement metadata only, no raw audio/transcripts) feeding a future NIH R01 application

**🔬 HPC + ML Research at SLU HPC Lab (M.S. CS, Dec 2026):**
- Federated Learning parallelization with empirical Amdahl analysis (1.27× stable speedup, ~24% parallel fraction ceiling proven); now extending to multi-node FL + FedAsync on the SLU Libra cluster
- Gaussian Process Regression + LSTM pipeline for clinical force prediction with uncertainty estimation, on NVIDIA L40S under SLURM
- CARLA distributed autonomous-driving data collection with GIST (2 nodes × 8 A100, SLURM + Singularity) — contributed the watchdog + auto-resubmission job chain; targeting an SC2026 workshop paper

**☁️ Production AWS at scale (4 years at Doverunner):**
- Redesigned a synchronous-RDB watermark token system into a **Lambda + Redis + SNS** architecture → **5M+ race-free tokens** across Seoul, Oregon, Frankfurt with **30% peak-latency reduction**
- Replaced a Hybrik-based encoding SaaS with a self-hosted **AWS EKS** pipeline → **50% cost cut, 30% throughput lift**
- Reduced 100-user video conference room initialization from 0.6s to 0.1s — a **6× user-facing latency improvement** at TmaxWAPL

## 📩 What I'm Looking For

Mid-level (SDE II / SWE II) roles in:
- ☁️ Cloud / Distributed Systems Infrastructure
- 🤖 ML / AI Platform Engineering
- 🎬 Video / Streaming Infrastructure
- 🏥 Healthcare AI

📍 St. Louis, MO | Open to relocation anywhere in the U.S. | F-1 OPT + 3-year STEM extension eligible | Available **January 2027**

→ Reach me via [LinkedIn](https://www.linkedin.com/in/seungbum-jung-6a105317a/) or email tofoth@gmail.com.

## Research

### ✅ Clinical LLM Chatbot for MCI Patient Support — **Ongoing (funded RA, Summer 2026 →)**
- Funded RA project at SLU HPC Lab (advisor: Prof. Ted Ahn) — an **iPad-based conversational AI** for patients with **Mild Cognitive Impairment (MCI)**, deployed in a **HIPAA-compliant** clinical setting as a feasibility pilot supporting a future **NIH R01** application. Code private (clinical constraints)
- **Working prototype complete**: device pairing, patient onboarding, AI-initiated proactive conversation, coordinator dashboard with CSV export, de-identified UUID participant labels — covered by **204 Vitest tests**
- **Safety enforced server-side**: crisis detection with Code Blue escalation and a 988-crisis lockout flow, plus prompt-level guardrails. Data architecture captures engagement metadata only — **no raw audio or full conversation transcripts**
- **Voice interaction in design**: turn-based, server-relayed voice via AWS Transcribe / Polly — hybrid voice + screen for older-adult accessibility. Pilot: ~15 participants, 6 months, two variants (neutral vs proactive)  
  **Stack:** OpenAI / Claude APIs, prompt engineering + safety guardrails, iPad (frontend), institutional backend (HIPAA), AWS Transcribe / Polly (voice, in design), Vitest

### ✅ Distributed Autonomous-Driving Data Collection on HPC (CARLA) — **Ongoing, with GIST AIGS**
- Run CARLA simulation workloads across **2 nodes × 8 NVIDIA A100 GPUs**, scheduled with **SLURM** and containerized with **Singularity**, collecting data for the **LAV** and **InterFuser** autonomous-driving pipelines
- Contributed the **watchdog + automatic-resubmission job chain** so long-running collection jobs survive transient failures without manual intervention
- Targeting an **SC 2026 workshop paper**  
  **Stack:** CARLA, SLURM, Singularity, NVIDIA A100, Python

### ✅ Parallelizing Federated Learning Client Simulation [📄 Read More](https://github.com/back99/fl-simulation)
- **Identified** the single-process bottleneck capping FL research throughput; **prototyped** Python `ProcessPoolExecutor` parallelization and **diagnosed** a PyTorch tensor-pickling deadlock at the IPC boundary, **resolving** it via NumPy serialization
- **Measured ~1.27× stable speedup** across 50–200 Non-IID MNIST clients on an 8-core CPU; **proved** an Amdahl ceiling (~24% parallel fraction), pointing the next iteration to multi-node FL rather than further single-machine tuning
- In progress: scaling FL to multi-node SLU Libra HPC and Asynchronous FedAvg (FedAsync-style); planned: CIFAR-10 + ResNet-18 workloads  
  **Stack:** Python, PyTorch, NumPy, multiprocessing, MNIST, FedAvg

### ✅ Dental Aligner ML Force Prediction [📄 Read More](https://github.com/back99/dental-ml-force-prediction)
- **GPR for thickness extrapolation**: Found XGBoost collapsed to flat lines outside the training range (0.25/0.5mm), useless for predicting forces (Fx–Fz, Tx–Tz) on U6/U7 molars at unseen thicknesses (0.75/1.0/1.25mm). Re-architected with **Gaussian Process Regression** (Matern kernel) for **μ ± 2σ** uncertainty; augmented training with weighted-delta-method synthetic 0.75mm data to distinguish 1.0 vs 1.25mm predictions
- **LSTM LOO + Partial Observation forecasting**: Reframed as "given a new patient's early measurements, forecast later force/moment trajectory." Designed a **60-experiment matrix** (5 cohorts × 3 horizons × 4 sheets) — train on 4 other cohorts plus target cohort's first (11−k) points, predict the last k ∈ {1,2,3} points
- **Model**: LSTM(128, 2 layers, dropout 0.2) → Dense(64) → scalar, 300 epochs with StepLR
- **Complementary design**: GPR covers **spatial** extrapolation (thickness), LSTM covers **temporal** extrapolation (14-day window). Trained on **NVIDIA L40S** GPUs under **SLURM** on the SLU Libra HPC cluster  
  **Stack:** Python, PyTorch, GPyTorch, XGBoost, scikit-learn, pandas, numpy, SLURM

## Experience

### ✅ Watermark Token Issuance Optimization [📄 Read More](Watermark_session_token_ver2)
> **Redesigned** the legacy synchronous-RDB token service into a non-linear-index Lambda + Redis + SNS event-driven architecture, **to fix** peak-time latency spikes and regional index collisions blocking scale-out, **delivering 30% peak-latency reduction and 5M+ race-free tokens** across Seoul, Oregon, and Frankfurt.

**Stack:** Kotlin, AWS Lambda, Redis, SNS, CloudWatch, RDS

### ✅ Distributed Encoding System on AWS EKS [📄 Read More](Distributed_transcoding)
> **Designed and built** a containerized encoding pipeline on AWS EKS with GOP-aware video partitioning and Redis-based job control with auto-failover, **to replace** a Hybrik-based external SaaS that was cost-prohibitive and inelastic at scale, **cutting encoding cost 50% and lifting throughput 30%**.

**Stack:** Kotlin, Spring Boot, AWS EKS, Docker, Redis, FFmpeg

## Education

- **M.S. in Computer Science (in progress)** — Saint Louis University, USA, Aug 2025 – Dec 2026 (expected)  
  Advisor: Prof. Ted Ahn · Lab: High Performance Computing Lab · GPA: 3.63 / 4.0
- **B.S. in Computer Engineering** — Ajou University, South Korea, 2015–2018

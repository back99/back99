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
- Clinical LLM companion for older adults with MCI at SLU HPC Lab (research prototype, pilot after IRB approval) — [Read More](https://github.com/back99/mci-chatbot-showcase)
- **LLM design:** safety handled outside the model (rule-based crisis check before every LLM call; the AI second pass can only raise risk), prompts assembled from reviewable config files, prompt caching, post-session LLM metadata extraction
- **AI-driven development:** built with a Claude Code multi-agent team (lead, server, frontend, mobile, AI, QA); I owned requirements, task design, PR review and merge, and AWS operations

**🔬 HPC + ML Research at SLU HPC Lab (M.S. CS, Dec 2026):**
- Federated Learning parallelization with empirical Amdahl analysis (1.27× stable speedup, ~24% parallel fraction ceiling proven); now extending to multi-node FL + FedAsync on the SLU Libra cluster
- Gaussian Process Regression + LSTM pipeline for clinical force prediction with uncertainty estimation, on NVIDIA L40S under SLURM
- HPC-CARLA: closed-loop evaluation of autonomous-driving agents on HPC with GIST (2 nodes × 8 A100, SLURM + Singularity) — contributed the watchdog + auto-resubmission job chain; co-authored paper accepted at WORKS 2026 (SC26 workshop)

**☁️ Production AWS at scale (DoveRunner, 2023–2025):**
- Redesigned a synchronous-RDB watermark token system into a **Lambda + Redis + SQS/SNS** architecture → **5M+ tokens issued** across Seoul and Oregon, later Frankfurt, with a **30% latency reduction**
- Built a self-hosted **AWS EKS** transcoding pipeline replacing a Hybrik-based SaaS → **50% cost cut, 30% throughput lift**; owned GOP-aware segmentation, transcoding workers, and segment merge
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

### ✅ Clinical LLM Chatbot for MCI Patient Support — **Research prototype (funded RA, Summer 2026 →)** [📄 Read More](https://github.com/back99/mci-chatbot-showcase)
- iPad-based voice conversation companion for older adults with **Mild Cognitive Impairment (MCI)**, built at SLU HPC Lab as groundwork for a clinical feasibility pilot supporting a future **NIH R01** application. Pilot planned after IRB approval; code private (clinical constraints)
- **How the LLM is used (design):**
  - **Safety outside the model:** every message passes a rule-based crisis check before any LLM call; a crisis signal stops the conversation and starts a lock → safety question → 911/988 → staff alert flow that only a person can clear. A context filter cuts false positives, and the AI second pass can only raise the risk level
  - **Prompts as config:** persona, always-on safety rules, participant context, a topic bank, and a 5-minute wrap-up instruction are separate files assembled per request, so the PI can review and edit them without code changes. Prompt caching on the fixed system prompt; LLM usage and cost visible in the staff dashboard
  - **LLM after the session:** the model extracts topics and clinical-domain flags as research metadata; raw transcripts and audio are not stored in the database
  - **Voice latency:** AWS Transcribe + Polly with per-sentence TTS and speculative early STT, about 1.3–1.6 s to first audio on dev; chose the Polly engine with ~1.0 s vs 2.7–2.9 s
- **How it was built (AI-driven development):** a Claude Code multi-agent team (lead, server, frontend, mobile, AI, QA) working task → branch → PR → QA → merge. Safety logic, session limits, and interface changes require my approval; I owned requirements with the PI, PR review and merge, and AWS infrastructure (EC2, Docker Compose, GitHub Actions)  
  **Stack:** FastAPI, React + TypeScript, PostgreSQL, Claude API, AWS (Transcribe, Polly, EC2), Docker, GitHub Actions

### ✅ HPC-CARLA: Closed-Loop Evaluation of Autonomous-Driving Agents on HPC — **Paper accepted at WORKS 2026 (SC26 workshop), with GIST AIGS** [📄 Read More](https://github.com/back99/HPC-CARLA)
- Co-authored (2nd author) a system that runs **closed-loop CARLA evaluation** of six public agents (TCP, InterFuser, CILRS, NEAT, Roach, LAV) as declarative YAML pipelines over one stage library, across **2 nodes × 8 NVIDIA A100 GPUs** with **SLURM** and **Singularity/Apptainer**
- Contributed the **watchdog + automatic-resubmission job chain** so long-running evaluation jobs survive crashes and allocation expiry without manual intervention
- System results: persistent per-GPU CARLA servers reuse the ~120s boot across jobs; episode-granular accounting recovered **94% of 13,059 route evaluations** from jobs that job-level accounting would have discarded  
  **Stack:** CARLA, SLURM, Singularity/Apptainer, NVIDIA A100, Python

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

## Side Projects

### ✅ Crypto Lead-Lag Strategy Validation [📄 Read More](https://github.com/back99/coin-leadlag-validation)
- Tested the day-trading idea "altcoins follow BTC/ETH with a delay" against real market data **before building any trading bot**: Upbit 5-minute bars (90 days), Binance 1-second bars (2 days), and Upbit/Bithumb order books via public REST APIs
- Every test used a **random-entry control group, in-sample/out-of-sample split, and per-coin measured round-trip cost**; each tool was first checked on synthetic data with a planted signal
- **All 9 strategies rejected**: altcoins follow BTC almost instantly (correlation ~0.01 one minute later), so the signal (~+0.1%) never beats the round-trip cost (0.115% to 1.022%); trend following went from +27.7% in-sample to -31.0% out-of-sample
- Built with an AI assistant (Claude): I set the hypotheses, ran the scripts, and caught flaws in the AI's analysis (fixed-time exits recording a +1.10% win as -0.20%, and ignoring per-pair beta); the AI wrote the code. No real trading  
  **Stack:** Python, pandas, NumPy, Upbit / Binance / Bithumb APIs

## Experience

### ✅ Watermark Token Issuance Optimization [📄 Read More](Watermark_session_token_ver2)
> **Redesigned and built** the synchronous-RDB token service on a non-linear-index Lambda + Redis + SQS/SNS architecture, **to fix** slow issuance under heavy traffic and cross-region index collisions blocking scale-out, **delivering a 30% latency reduction and 5M+ tokens issued** across Seoul and Oregon, later extended to Frankfurt.

**Stack:** Kotlin, AWS Lambda, Redis, SQS, SNS, CloudWatch, RDS

### ✅ Distributed Encoding System on AWS EKS [📄 Read More](Distributed_transcoding)
> **Built** a containerized encoding pipeline on AWS EKS, owning GOP-aware video partitioning, transcoding workers, and segment merge, **to replace** a Hybrik-based external SaaS that was cost-prohibitive and inelastic at scale, **cutting encoding cost 50% and lifting throughput 30%**.

**Stack:** Kotlin, Spring Boot, AWS EKS, Docker, Redis, FFmpeg

## Education

- **M.S. in Computer Science (in progress)** — Saint Louis University, USA, Aug 2025 – Dec 2026 (expected)  
  Advisor: Prof. Ted Ahn | Lab: High Performance Computing Lab | GPA: 3.67 / 4.0
- **B.S. in Computer Engineering** — Ajou University, South Korea, 2015–2018

# Hi, I'm Seung Bum Jung

## About Me

Hello! I'm Seung Bum Jung — a backend engineer with several years of experience, currently pursuing a Master's in Computer Science at Saint Louis University.

I specialize in designing scalable distributed systems, and I'm expanding into AI/ML engineering — particularly Federated Learning and distributed AI infrastructure. My goal is to bridge hands-on industry experience with applied AI research to build systems that work at scale in the real world.

Before grad school, I worked as a backend developer building scalable media processing pipelines and high-performance distributed systems. At SLU, I'm conducting research on parallelizing Federated Learning and collaborating on distributed autonomous driving simulation with GIST.

## Research

### ✅ Parallelizing Federated Learning Client Simulation [📄 Read More](https://github.com/back99/fl-simulation)
- Parallelized FL client training using Python `ProcessPoolExecutor`, achieving up to **1.27x speedup** over serial baseline
- Solved PyTorch tensor pickling deadlock via NumPy serialization for inter-process communication
- Implemented Non-IID data partitioning and FedAvg aggregation on MNIST across 10–50 clients.  
  **Stack:** Python, PyTorch, NumPy, multiprocessing

### ✅ Dental Aligner ML Force Prediction [📄 Read More](https://github.com/back99/dental-ml-force-prediction)
- Predicted orthodontic forces (Fx, Fy, Fz, Tx, Ty, Tz) at unseen aligner thicknesses (0.75/1.0/1.25mm) on **U6/U7 molars**, using real 0.25mm and 0.5mm DPA experimental data (Smith dataset)
- Identified XGBoost's extrapolation limitation (flat-line predictions beyond training range) and switched to **Gaussian Process Regression (GPR)** with Matern kernel (ν=1.5) for principled uncertainty estimates (μ ± 2σ)
- Generated simulated 0.75mm data via a **weighted delta method** (w = 0.5~1.5) to augment GPR training — enabled the model to distinguish 1.0mm vs 1.25mm predictions, which collapsed to flat lines on real-data-only training
- Trained on **NVIDIA L40S (48GB VRAM)** GPUs via GPyTorch, scheduled with **SLURM** on the Libra HPC cluster  
  **Stack:** Python, PyTorch, GPyTorch, XGBoost, scikit-learn, pandas, numpy, matplotlib, seaborn, SLURM

## Experience

### ✅ Distributed Transcoding [📄 Read More](Distributed_transcoding)
- Designed a scalable video transcoding system to replace Hybrik, reducing costs by 50% and improving throughput by 30%.
- Deployed parallel transcoding pods on AWS EKS based on GOP-aware segmentation.
- Used Redis for job queuing and failure recovery; modularized packaging and media services for maintainability.  
  **Stack:** Kotlin, Spring Boot, AWS EKS, Redis, Docker, FFmpeg

### ✅ Watermark Session Token Optimization [📄 Read More](Watermark_session_token_ver2)
- Rebuilt token generation with Redis and AWS Lambda for low-latency issuance (↓30%).
- Implemented a globally unique token strategy across Seoul, Oregon, and Frankfurt.
- Integrated event-based regeneration via SNS and CloudWatch, enabling 5M+ token support.  
  **Stack:** Kotlin, Redis, AWS Lambda, CloudWatch, SNS

### ✅ Legacy API Refactoring & Kotlin Migration
- Refactored legacy Java APIs to Kotlin with DDD structure and handler-resolver pattern.
- Improved interface design, testability, and async communication via Kafka.
- Boosted developer onboarding speed and deployment maintainability.  
  **Stack:** Kotlin, Spring Boot, Kafka, DDD

### ✅ CMS System Optimization
- Refactored Redis caching and pub/sub architecture for collaboration tools.
- Reduced CMS latency and increased cache hit ratio by cleaning stale keys and streamlining logic.
- Modularized chat, alarm, and account services for future scalability.  
  **Stack:** Java, Redis, Spring Boot, Pub/Sub

## Education

- **Master’s in Computer Science (in progress)**  
  *(Saint Louis University, USA, 2025–2026 expected)*

- **B.S. in Computer Engineering, Ajou University, South Korea**

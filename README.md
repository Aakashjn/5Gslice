
---

# 🛡️ SliceShield: Edge AI for 5G Network Slice Security 

---

## 📌 Overview

SliceShield is a next-generation security framework designed to protect **5G Service-Based Architecture (SBA)** network slices using **Edge Artificial Intelligence (AI)** and **Federated Learning (FL)**.

The framework provides real-time detection, automated mitigation, and intelligent forensic analysis of cyber threats targeting different 5G network slices. By leveraging decentralized learning, SliceShield eliminates the need for centralized raw data sharing while maintaining high detection accuracy and privacy preservation.

### Key Objectives

* Secure 5G network slices against advanced cyberattacks.
* Enable privacy-preserving decentralized model training.
* Detect threats in real time using Edge AI.
* Automatically isolate malicious traffic using Software Defined Networking (SDN).
* Generate AI-powered Root Cause Analysis (RCA) reports for incident investigation.

---

# 🚀 Key Features

| Feature                 | Description                                           |
| ----------------------- | ----------------------------------------------------- |
| Federated Learning      | Decentralized model training without sharing raw data |
| Edge AI Detection       | Low-latency anomaly detection at edge nodes           |
| Real-Time Monitoring    | Continuous monitoring of network traffic              |
| Automated Response      | Immediate threat containment and isolation            |
| SDN Integration         | Dynamic OpenFlow rule deployment                      |
| AI-Powered RCA          | Automated forensic report generation                  |
| Dashboard Visualization | Live attack and telemetry monitoring                  |
| Recovery Monitoring     | Automatic restoration after clean traffic windows     |

---

# 🏗️ System Architecture

The SliceShield framework operates through a four-layer defensive architecture:

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        5G Network Control Plane                        │
│   eMBB Slice (0)            URLLC Slice (1)           mMTC Slice (2)   │
└───────┬────────────────────────────┬───────────────────────────┬───────┘
        │                            │                           │
        ▼                            ▼                           ▼
┌────────────────────────────────────────────────────────────────────────┐
│ LAYER 1: DATA PIPELINE                                                 │
│ - Deep Packet Inspection (DPI)                                         │
│ - Feature Extraction                                                   │
│ - Traffic Decoding                                                     │
└────────────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌────────────────────────────────────────────────────────────────────────┐
│ LAYER 2: FEDERATED LEARNING                                            │
│ - Distributed Edge Training                                            │
│ - Flower Framework                                                     │
│ - Differential Privacy Support                                         │
└────────────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌────────────────────────────────────────────────────────────────────────┐
│ LAYER 3: DETECTION ENGINE                                              │
│ - Neural Network Inference                                             │
│ - Sliding Window Evaluation                                            │
│ - Anomaly Scoring                                                      │
└────────────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌────────────────────────────────────────────────────────────────────────┐
│ LAYER 4: RESPONSE ENGINE                                               │
│ - SDN-Based Traffic Isolation                                          │
│ - Circuit Breaker Protection                                           │
│ - Recovery Monitoring                                                  │
└────────────────────────────────────────────────────────────────────────┘
```

---

# 🔄 Security Workflow

```text
Traffic Collection
        │
        ▼
Feature Extraction
        │
        ▼
Federated Learning
        │
        ▼
Anomaly Detection
        │
        ▼
Threat Identification
        │
        ▼
Automated Mitigation
        │
        ▼
Root Cause Analysis
        │
        ▼
Recovery Monitoring
```

---

# 📂 Project Structure

```text
5gdemo/
├── launcher.py
├── dashboard_server.py
├── run_pipeline.py
├── data_pipeline.py
├── fl_trainer.py
├── detection_engine.py
├── response_engine.py
├── rca_agent.py
├── attack_simulation.py
├── packet_sniffer.py
├── malicious_data.csv
├── models/
└── logs/
```

---

# 📖 Component Description

### launcher.py

Acts as the central orchestrator for the entire framework. It launches and manages all project services, monitors process health, and performs graceful shutdown operations.

### dashboard_server.py

Hosts the Flask and Socket.IO-based dashboard responsible for real-time monitoring and visualization of security events.

### run_pipeline.py

Coordinates communication between detection modules, mitigation systems, and monitoring services.

### data_pipeline.py

Processes raw network data and converts packet streams into machine-learning-ready feature vectors.

### fl_trainer.py

Implements Federated Learning using Flower and PyTorch for distributed edge-based model training.

### detection_engine.py

Performs anomaly detection using trained neural network models and rule-based fallback mechanisms.

### response_engine.py

Handles automatic mitigation by deploying SDN/OpenFlow rules and maintaining slice isolation policies.

### rca_agent.py

Uses Large Language Models (LLMs) through the Groq API to generate Root Cause Analysis reports.

### attack_simulation.py

Simulates cyberattacks for testing and evaluating system performance.

### packet_sniffer.py

Captures live traffic and extracts real-time features for analysis.

---

# ⚙️ System Requirements

## Hardware

* Minimum 8 GB RAM
* Dual-Core Processor
* 5 GB – 10 GB Free Storage

## Software

* Ubuntu 20.04 LTS or newer
* Python 3.10+
* Apache Kafka (Optional)
* Open vSwitch (Optional)
* Groq API Key (Optional)

---

# 🔧 Installation

## Step 1: Clone Repository

```bash
git clone https://github.com/your-repository/SliceShield.git
cd SliceShield
```

## Step 2: Create Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

## Step 3: Upgrade Package Manager

```bash
pip install --upgrade pip setuptools wheel
```

## Step 4: Install Dependencies

```bash
pip install torch flwr flask flask-socketio flask-cors kafka-python scapy scikit-learn pandas numpy requests
```

---

# 🧠 Federated Learning Training

Before running the system, train the Federated Learning model.

```bash
python launcher.py --train --no-browser
```

Training performs:

* Dataset preprocessing
* Client partitioning
* Local edge training
* Global model aggregation
* Model export

Generated model:

```text
models/federated_model.pt
```

---

# 🤖 AI Forensics Configuration

To enable automated Root Cause Analysis generation:

```bash
export GROQ_API_KEY="YOUR_GROQ_API_KEY"
```

The framework will use:

```text
llama-3.1-8b-instant
```

to generate forensic investigation reports.

---

# ▶️ Running SliceShield

Launch the complete security stack:

```bash
python launcher.py
```

This automatically starts:

* Dashboard Server
* Detection Engine
* Response Engine
* RCA Agent
* Browser Dashboard

Dashboard URL:

```text
http://localhost:5002
```

---

# 🧪 Attack Simulation

## Simulate NoSQL Injection

```bash
python attack_simulation.py --slice 1 --attack nosql
```

Target:

```text
URLLC Slice (1)
```

---

## Simulate DDoS Attack

```bash
python attack_simulation.py --slice 0 --attack ddos
```

Target:

```text
eMBB Slice (0)
```

---

# 🛡️ Automated Mitigation Actions

| Attack Type      | Response              |
| ---------------- | --------------------- |
| DDoS             | Traffic Isolation     |
| HTTP Flood       | Flow Blocking         |
| NoSQL Injection  | Session Termination   |
| Port Scan        | Slice Quarantine      |
| Lateral Movement | Access Restriction    |
| Service Abuse    | Dynamic Rate Limiting |

---

# 📊 Detection Process

The Detection Engine operates using:

### Sliding Window Analysis

```text
Window Size = 5
Overlap = 2
```

### Detection Logic

1. Collect telemetry records.
2. Generate feature vectors.
3. Run neural network inference.
4. Compute anomaly probability.
5. Compare against threshold.
6. Trigger alert if threshold exceeded.

Default Threshold:

```text
0.65
```

---

# 🔐 Federated Learning Workflow

```text
Edge Client 1
       │
Edge Client 2
       │
Edge Client 3
       │
       ▼
Flower Aggregator
       │
       ▼
Global Model
       │
       ▼
Deployment
```

Benefits:

* Data Privacy
* Reduced Bandwidth Usage
* Improved Scalability
* Distributed Intelligence

---

# 📈 Dashboard Features

The monitoring dashboard displays:

* Slice Health Status
* Threat Alerts
* Isolation Events
* Detection Metrics
* Traffic Statistics
* RCA Reports
* Recovery Status

---

# 📋 Configuration Parameters

| Component           | Parameter          | Default |
| ------------------- | ------------------ | ------- |
| detection_engine.py | threshold          | 0.65    |
| detection_engine.py | window_size        | 5       |
| response_engine.py  | max_isolations_min | 3       |
| response_engine.py  | clean_windows_req  | 3       |
| response_engine.py  | clean_threshold    | 0.30    |
| response_engine.py  | ssh_port           | 2222    |
| packet_sniffer.py   | sbi_port           | 7777    |

---

# 📊 Evaluation Metrics

The framework can be evaluated using:

* Accuracy
* Precision
* Recall
* F1-Score
* False Positive Rate
* Detection Latency
* Mitigation Time
* Recovery Time

---

# 🔮 Future Enhancements

* Kubernetes-Based Deployment
* Real 5G Core Integration
* Explainable AI Module
* Blockchain Trust Management
* Multi-Cloud Federated Learning
* Threat Intelligence Sharing
* Advanced SDN Orchestration
* Edge Container Security

---

# 👨‍💻 Project Team

### SliceShield Development Team

* Hemanth
* Aakash
* Nikhath
* Sakhi

**Department of Information Science and Engineering**

---

# 📜 License

This project is developed for academic and research purposes.

Copyright © 2026 SliceShield Research Team.

---

**SliceShield combines Edge AI, Federated Learning, SDN Automation, and AI-Powered Forensics to deliver a complete zero-trust security solution for next-generation 5G network slicing environments.** 

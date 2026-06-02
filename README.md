# SliceShield: Edge AI for 5G Network Slice Security (ISP81)
### Department of Information Science and Engineering (ISE)
**Project Team:** Hemanth • Aakash • Nikhath • Sakhi

---

## 1. Architectural Overview

SliceShield is a complete, multi-layered zero-trust security framework designed for next-generation 5G Service Based Architectures (SBA). It uses **Edge AI** and **Federated Learning** to protect network slices from critical exploits without requiring centralized raw data sharing.

The system is organized into a four-layer real-time defensive loop:

┌────────────────────────────────────────────────────────────────────────┐
│                        5G Network Control Plane                        │
│   eMBB Slice (0)            URLLC Slice (1)           mMTC Slice (2)   │
└───────┬────────────────────────────┬───────────────────────────┬───────┘
│                            │                           │
▼ (Live Packet Tapping)      ▼ (Kafka Streams)           ▼ (OVS Bridges)
┌────────────────────────────────────────────────────────────────────────┐
│ LAYER 1: DATA PIPELINE (data_pipeline.py / packet_sniffer.py)     │
│  - Real-time deep packet inspection (DPI) of 5G SBI protocols via Scapy│
│  - Hex decoding, HTTP/2 state matching, and 20-dimensional feature extraction
└───────┬────────────────────────────────────────────────────────────────┘
│
▼ (Balanced NumPy/CSV Datasets)
┌────────────────────────────────────────────────────────────────────────┐
│ LAYER 2: FEDERATED LEARNING (fl_trainer.py)                         │
│  - Decentralized training across virtual edge client nodes via Flower  │
│  - Privacy preservation using optional DP-SGD (Differential Privacy)   │
│  - Aggregated global weight synthesis utilizing the FedAvg strategy    │
└───────┬────────────────────────────────────────────────────────────────┘
│
▼ (models/federated_model.pt)
┌────────────────────────────────────────────────────────────────────────┐
│ LAYER 3: DETECTION ENGINE (detection_engine.py)                      │
│  - Rolling window evaluation mechanics (Size = 5, Overlap = 2)         │
│  - Fast PyTorch neural network matrix inference                        │
│  - Heuristic algorithmic rule fallback logic when un-trained          │
└───────┬────────────────────────────────────────────────────────────────┘
│
▼ (Real-time Anomaly Signals)
┌────────────────────────────────────────────────────────────────────────┐
│ LAYER 4: AUTOMATED RESPONSE ENGINE (response_engine.py)             │
│  - Dynamic playbook mitigation lookups (DDoS, NoSQL, Lateral Movement)  │
│  - Multi-process token bucket Circuit Breaker configuration            │
│  - Remote Open vSwitch (OVS) rule injection over out-of-band SSH       │
│  - Active state recovery monitoring via strict trailing clean windows   │
└────────────────────────────────────────────────────────────────────────┘


---

## 2. Directory Structure & Complete File Manifest

Ensure your project environment matches this exact structure:

5gdemo/
├── launcher.py               # Unified multi-process startup orchestrator
├── dashboard_server.py       # Flask + Socket.IO telemetry dashboard server (Port 5002)
├── run_pipeline.py           # Core detection & response execution loop
├── data_pipeline.py          # Training dataset builder and offline decoder
├── fl_trainer.py             # Flower + PyTorch federated learning implementation
├── detection_engine.py       # Stream ingestion and inference evaluation layer
├── response_engine.py        # Mitigation playbooks, SDN control, and recovery loops
├── rca_agent.py              # LLM forensics text analyzer (Groq Cloud API integration)
├── attack_simulation.py      # Telemetry injection tool for stress testing
├── packet_sniffer.py         # Live Scapy-based network tap to Kafka pipeline
├── malicious_data.csv        # Core exploit sample dataset (must be present)
├── models/                   # Generated automatically after Federated training
└── logs/                     # Created dynamically to handle audit trails and events


### Detailed Component Deep-Dive

* **`launcher.py`**: The main control entry point. It handles process group lifecycle management, captures interleaved stdout/stderr streams, prefixes lines with ANSI color headers, monitors process health, auto-restarts crashed threads, and handles graceful signal cleanups (`SIGINT`, `SIGTERM`).
* **`dashboard_server.py`**: Replaces old legacy API architectures. It runs a non-blocking log tailer on a background thread that watches the audit trails, broadcasting modifications directly to the web canvas via high-speed asynchronous Socket.IO WebSockets.
* **`run_pipeline.py`**: The runtime coordinator. It performs dependency audits, checks environment files, and links the inference pipeline directly to execution pathways based on the configuration mode (`demo` vs `kafka`).
* **`data_pipeline.py`**: Cleans the raw byte streams in `malicious_data.csv`. It parses hexadecimal payloads into string packets, tracks specific fields (like target IMSIs, NoSQL operators, and NRF paths), balances classes with synthetic standard data, and partitions data into designated network slice profiles:
    * **Slice 0 (eMBB)**: Configured to process volumetric attacks (DDoS, HTTP floods).
    * **Slice 1 (URLLC)**: Configured to monitor transaction anomalies (NoSQL injection, application tampering).
    * **Slice 2 (mMTC)**: Configured to intercept internal discovery exploits (Port scans, lateral movement).
* **`fl_trainer.py`**: A simulator for training edge clients. Each client trains locally on its slice data using multi-layered Batch Normalization and Dropout layers before sending updates to a `FedAvg` central aggregator via Flower server instances[cite: 13].
* **`detection_engine.py`**: Operates on a sliding micro-batch buffer[cite: 13]. When a slice queue accumulates 5 records, it computes the mean probability score across the window[cite: 13]. If the score matches or exceeds the 0.65 threshold, it raises an alert[cite: 13]. If a model file isn't available, it falls back to a rule-based heuristic scanner[cite: 13].
* **`response_engine.py`**: The defensive mitigation engine[cite: 13]. It uses a custom SSH abstraction layer to execute OpenFlow rules directly on an OVS bridge, instantly dropping malicious traffic[cite: 13]. A circuit breaker blocks system cascades if more than 3 mitigations occur in a single minute, while a recovery monitor automatically restores access after 3 consecutive clean windows[cite: 13].
* **`rca_agent.py`**: An automated forensic analyst[cite: 13]. It processes raw incident logs and queries the Groq API using `llama-3.1-8b-instant` to generate thorough Markdown root cause analysis reports[cite: 13].
* **`packet_sniffer.py`**: A live capture tool that filters traffic on Port 7777, extracts identical 20-dimensional feature arrays in real time, and publishes JSON records directly to local or remote Apache Kafka messaging clusters[cite: 13].

---

## 3. Environment Provisioning & Installation

### Infrastructure Requirements
* **Operating System**: Linux (Ubuntu 20.04 LTS or newer highly recommended)[cite: 13].
* **Storage Overhead**: **5.0 GB – 10.0 GB** of free system space on the target path[cite: 13]. This clearance is strictly mandatory to accommodate heavy dependencies like `torch` and wheel builds[cite: 13].

### Step-by-Step Installation

1. Navigate to the consolidated project root[cite: 13]:
```bash
   cd ~/Documents/5gdemo
Initialize and isolate a clean Python 3 environment[cite: 13]:

Bash
   python3 -m venv venv
   source venv/bin/activate
Update core packaging tools[cite: 13]:

Bash
   pip install --upgrade pip setuptools wheel
Install the required dependency stack[cite: 13]:

Bash
   pip install torch flwr flask flask-socketio flask-cors kafka-python scapy scikit-learn pandas numpy requests
4. Operational Run Guide
Execution Workflow
[Step 1: Train Model] ──► [Step 2: Export Groq Key] ──► [Step 3: Launch Stack]
  ( launcher.py --train )      ( export GROQ_API_KEY )        ( launcher.py )
Step 1: Model Initialization & Federated Training
If models/federated_model.pt is not present, you must initialize the decentralized training run across the slice datasets[cite: 13]:

Bash
python launcher.py --train --no-browser
Monitor the terminal output to confirm that the training progresses through all 10 Flower aggregation rounds[cite: 13]. Once the final global weight configuration is successfully exported, terminate the training process by pressing Ctrl+C[cite: 13].

Step 2: Configure the Forensics Engine (Optional)
To enable the automated AI Root Cause Analysis report generation feature, export your Groq Cloud API access token into your active environment shell[cite: 13]:

Bash
export GROQ_API_KEY="your_actual_groq_api_token_string"
Step 3: Launch the Full Active Protection Stack
Start the live system using the primary launcher utility[cite: 13]:

Bash
python launcher.py
This command automatically brings up the following background processes[cite: 13]:

Dashboard Engine: Initializes the web-server runtime on Port 5002[cite: 13].

Pipeline Core: Provisions detection logic buffers and prepares SDN control pathways[cite: 13].

Forensics Agent: Launches log tailing and prepares Groq API connectors[cite: 13].

Browser Interface: Automatically opens the dashboard at http://localhost:5002[cite: 13].

5. System Testing & Evaluation
Simulating Attack Behaviors
To evaluate the system's real-time detection and mitigation responses without a live network setup, use the automated simulation tool[cite: 13]. Open a separate terminal window, navigate to the project directory, activate the environment, and run an injection command[cite: 13]:

Inject a NoSQL Injection Exploit targeting the URLLC Slice (1):

[cite: 13]

Bash
    python attack_simulation.py --slice 1 --attack nosql
    ```

* **Inject a Volumetric DDoS Exploit targeting the eMBB Slice (0):**[cite: 13]
```bash
    python attack_simulation.py --slice 0 --attack ddos
    ```

### Expected Defensive System Actions
1. **Detection**: The engine identifies the anomalous signature inside the data window[cite: 13].
2. **SDN Containment**: The Response Engine connects to the network bridge over SSH and applies a rule to drop the malicious traffic within milliseconds[cite: 13].
3. **Visual Update**: The web dashboard highlights the affected slice in red and updates the system metric counters[cite: 13].
4. **Forensics**: The RCA agent generates an incident report file named `RCA_Report_Slice<ID>_<Timestamp>.md` in the main folder[cite: 13].

---

## 6. System Configuration Reference

You can update key operational parameters directly in the configuration headers of the respective scripts[cite: 13]:

| Script Component | Configuration Parameter | Production Default | Functional Purpose |
| :--- | :--- | :--- | :--- |
| `detection_engine.py` | `threshold` | `0.65` | Sensitivity index threshold for neural net inference[cite: 13] |
| `detection_engine.py` | `window_size` | `5` | Length of sequential telemetry entries per slice evaluation window[cite: 13] |
| `response_engine.py` | `max_isolations_min` | `3` | Circuit-breaker protection cap for automated mitigations[cite: 13] |
| `response_engine.py` | `clean_windows_req` | `3` | Required consecutive clean windows before an isolated slice is readmitted[cite: 13] |
| `response_engine.py` | `clean_threshold` | `0.30` | Maximum anomaly score allowed for a window to be marked clean[cite: 13] |
| `response_engine.py` | `ssh_port` | `2222` | Out-of-band management connection port for OVS control plane access[cite: 13] |
| `packet_sniffer.py` | `sbi_port` | `7777` | Network interface port for monitoring Service Based Architecture traffic[cite: 13] |

---
*For execution issues or framework modifications, verify that your environment variables

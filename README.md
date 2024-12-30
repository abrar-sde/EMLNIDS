<h1 align="center">
EMLNIDS
</h1>


# Table of Contents

- [Introduction](#introduction)
- [Usage](#usage)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Features](#features)
- [Contributing](#contributing)
- [Documentation](#documentation)
- [Troubleshooting](#troubleshooting)

# EMLNIDS: Machine Learning-Based Intrusion Prevention System

EMLNIDS is an advanced intrusion prevention and detection system utilizing machine learning to analyze network traffic and detect malicious activities. It can process live traffic, PCAP files, and network flows from tools like Suricata and Zeek. EMLNIDS leverages multiple machine learning models, threat intelligence feeds, and custom heuristics to identify potential threats and mitigate them in real-time.

---

# Introduction

EMLNIDS is an open-source project designed to provide a robust, behavioral analysis-based intrusion prevention system. Initially inspired by behavioral intrusion detection systems, EMLNIDS employs machine learning models trained on various datasets to identify abnormal activities.

- **Supported platforms:** Linux, macOS (via Docker), and Windows (via Docker).
- **Blocking features:** Supported only on Linux.
- **Core dependencies:** Python 3.10, Zeek (for live traffic capture), and Redis (>= 7.0.4) for interprocess communication.

# Usage

### Linux and Windows Hosts
```bash
docker run --rm -it -p 55000:55000 \  
  --cpu-shares "700" --memory="8g" --memory-swap="8g" \  
  --net=host --cap-add=NET_ADMIN --name emlnids your-docker-repo/emlnids:latest
```

For manual traffic analysis:
```bash
./emlnids.py -f dataset/test.pcap -o output_dir
cat output_dir/alerts.log
```

### macOS Hosts
```bash
docker run --rm -it -p 55000:55000 \  
  --platform linux/amd64 --cpu-shares "700" \  
  --memory="8g" --memory-swap="8g" --cap-add=NET_ADMIN \  
  --name emlnids your-docker-repo/emlnids_macos:latest
```

---

# Requirements

EMLNIDS requires the following:
- Python 3.10.12
- At least 4GB of RAM
- Docker (recommended for ease of deployment)

---

# Installation

The recommended method to run EMLNIDS is via Docker. Steps for installation:

1. **Install Docker:** Ensure Docker is installed and running.
2. **Pull the Docker image:**
   ```bash
   docker pull your-docker-repo/emlnids:latest
   ```
3. **Run the container:**
   ```bash
   docker run --rm -it -p 55000:55000 \  
     --cpu-shares "700" --memory="8g" --memory-swap="8g" \  
     --net=host --cap-add=NET_ADMIN --name emlnids your-docker-repo/emlnids:latest
   ```

---

# Configuration

EMLNIDS relies on a configuration file (`config/emlnids.yaml`) that defines various options:

- **Analysis direction:** Set to `all` to analyze bidirectional traffic.
- **Machine learning mode:** Configure for `train` or `test` phases.
- **Time window:** Customize traffic analysis intervals by modifying the `time_window_width` parameter.

Detailed configuration options are available in the [official documentation](#documentation).

---

# Features

- **Behavioral Analysis:** Detect network anomalies using machine learning models.
- **Flexibility:** Analyze live traffic, PCAP files, or network flows.
- **Threat Intelligence Integration:** Use up-to-date threat intelligence feeds for accurate detection.
- **Cross-Platform:** Support for multiple operating systems through Docker.
- **User-Friendly Interfaces:** GUI for traffic analysis (web-based) and CLI (Kalipso).

---



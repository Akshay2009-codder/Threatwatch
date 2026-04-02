# 🛡️ ThreatWatch — AI-Based Insider Threat Prediction System

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Isolation%20Forest-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Processing-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Dashboard](https://img.shields.io/badge/Dashboard-HTML%2FJS%2FChart.js-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-00f5c4?style=for-the-badge)

**An unsupervised ML system that builds a 30-day behavioral baseline per employee,  
detects anomalies using Isolation Forest, and scores insider risk via a weighted IRI formula.**

[Features](#-features) · [Architecture](#-system-architecture) · [Installation](#-installation) · [Usage](#-usage) · [Dashboard](#-dashboard) · [Team](#-project-team)

---

> _Built at SSIP Cell, Government Polytechnic Palanpur — "New Palanpur for New India 4.0"_

</div>

---

## 📌 The Problem

| Traditional SIEM | ThreatWatch |
|---|---|
| Static rules only | Per-employee 30-day rolling baseline |
| Reacts after damage | Predictive — flags drift before breach |
| Manual, slow, expensive | Automated, real-time, open-source |
| Misses subtle behavioral drift | Isolation Forest catches subtle anomalies |
| No forecast capability | 7-day linear regression trend |

- **60%** of data breaches originate from inside the organization
- Threats unfold over weeks — not in single events
- Manual auditing is slow, costly, and human-error prone

---

## ✨ Features

- 🔍 **Unsupervised Anomaly Detection** — Isolation Forest requires zero labeled training data
- 📊 **Insider Risk Index (IRI)** — composite 0–100 score from 5 behavioral signal vectors
- 🧠 **Explainable AI** — plain-language explanations for every alert (XAI layer)
- ⚡ **Live Threat Simulation** — inject a rogue event and watch the model respond in real time
- 🖥️ **INSIGHT Dashboard** — cyberpunk SOC dashboard (pure HTML/JS, no backend needed)
- 📁 **Digital Twin** — real vs. predicted behavior comparison per employee
- 🤖 **AI SOC Analyst** — Gemini-powered natural language alert summaries *(future work)*

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      5-LAYER AI PIPELINE                        │
├──────────────┬──────────────┬────────────┬───────────┬──────────┤
│  Data Layer  │   Feature    │  ML Layer  │  Score    │    AI    │
│              │  Engineering │            │  Layer    │ Analyst  │
├──────────────┼──────────────┼────────────┼───────────┼──────────┤
│ Employee     │ Behavioral   │ Isolation  │ IRI       │ Gemini   │
│ Activity     │ Signal       │ Forest     │ (0–100)   │ SOC      │
│ Logs         │ Extraction   │ Model      │ Formula   │ Agent    │
│              │              │            │           │          │
│ login_hour   │ Normalize +  │ Unsuperv.  │ Weighted  │ Natural  │
│ files_access │ encode into  │ anomaly    │ composite │ language │
│ USB events   │ ML-ready     │ detection  │ scoring   │ alerts   │
│ sentiment    │ signals      │            │           │          │
└──────────────┴──────────────┴────────────┴───────────┴──────────┘
       ↓               ↓             ↓            ↓           ↓
  emp_workflow    emp_work.csv   IF Model     IRI Score   SOC Alert
     .log                        .pkl          0–100      plain EN
```

---

## 📐 Insider Risk Index — Scoring Formula

```
IRI = (AccessAnomaly × 0.40) + (BehavioralDrift × 0.35) + (SentimentShift × 0.25)
```

| Component | Weight | Signals Used |
|---|---|---|
| **AccessAnomaly** | 40% | `file_count_deviation` + `privilege_attempts` + `usb_events` |
| **BehavioralDrift** | 35% | `login_hour_deviation` + `login_location` + `sentiment_score` |
| **SentimentShift** | 25% | NLP score normalized to [−1, 1] |

**Risk Thresholds:**

| Score | Level | Action |
|---|---|---|
| ≥ 80 | 🚨 **Critical** | Escalate to HR + Security immediately |
| ≥ 60 | 🔴 **High** | Alert Security team, increase monitoring |
| ≥ 30 | 🟡 **Moderate** | Log for review, watch next 48 hours |
| < 30 | 🟢 **Low** | Normal baseline behavior |

---

## 📡 5 Behavioral Signal Vectors

```
File Access Volume      ████████████████████  40% weight
Login Time Anomaly      ████████████████      35% weight
Privilege Escalation    ████████              12% weight
USB / Data Exfiltration ████                   8% weight
Email Sentiment (NLP)   ██                     5% weight
```

---

## 🗂️ Project Structure

```
ThreatWatch/
│
├── 📄 data_preprocess.py         # Raw log → ML-ready CSV pipeline
├── 📄 train_model.py             # Isolation Forest training + scaler
├── 📄 score_employees.py         # IRI computation for all employees
│
├── 📁 data/
│   ├── emp_workflow.log          # Raw employee activity log (pipe-delimited)
│   └── emp_work.csv              # Preprocessed feature CSV (600 rows × 9 cols)
│
├── 📁 models/
│   ├── isolation_forest_model.pkl
│   └── scaler.pkl
│
├── 📄 app.py                     # Streamlit dashboard (legacy)
├── 📄 threatwatch_insight.html   # INSIGHT — standalone HTML/JS dashboard ✨
│
└── 📄 README.md
```

---

## ⚙️ Installation

### Prerequisites

- Python 3.10+
- pip

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/threatwatch.git
cd threatwatch
```

### 2. Install dependencies

```bash
pip install pandas numpy scikit-learn joblib
```

### 3. Run the data pipeline

```bash
# Step 1 — Preprocess raw log into CSV
python data_preprocess.py

# Step 2 — Train the Isolation Forest model
python train_model.py

# Step 3 — Score all employees and compute IRI
python score_employees.py
```

---

## 🚀 Usage

### Option A — INSIGHT Dashboard *(Recommended — no backend needed)*

Just open the HTML file directly in your browser:

```bash
open threatwatch_insight.html
# or double-click the file in your file manager
```

> No server, no Python, no installation. Works 100% offline.

### Option B — Streamlit App

```bash
pip install streamlit plotly
streamlit run app.py
```

Then visit `http://localhost:8501` in your browser.

### Option C — Score a new event programmatically

```python
from score_employees import score_new_row

rogue_event = {
    "login_hour"         : 2,      # 2 AM login
    "files_accessed"     : 230,    # mass download
    "privilege_attempts" : 9,      # hitting locked systems
    "emails_sent"        : 58,     # bulk email forwarding
    "usb_events"         : 1,      # USB plugged in
    "sentiment_score"    : -0.91   # hostile communications
}

score = score_new_row(rogue_event)
print(f"IRI Score: {score} / 100")   # → 97.3 / 100 — CRITICAL
```

---

## 🖥️ Dashboard — INSIGHT

**INSIGHT** is a standalone cyberpunk SOC dashboard with 4 screens:

| Screen | Description |
|---|---|
| 📊 **Leaderboard** | All 20 employees ranked by peak IRI, color-coded by risk level |
| 🔍 **Employee Deep Dive** | 30-day IRI timeline chart + signal breakdown + XAI explanations |
| 🚨 **Alert Panel** | Active critical/high threats + full response playbook |
| ⚡ **Live Simulation** | Inject a rogue event, watch the IRI compute in real time |

---

## 📊 Dataset

| Property | Value |
|---|---|
| Employees | 20 |
| Days per employee | 30 |
| Total records | 600 rows |
| Features | 9 (login_hour, files_accessed, privilege_attempts, emails_sent, usb_events, sentiment_score, anomaly_score, IRI, risk_label) |
| Anomalies detected | ~121 flagged days |
| Model | Isolation Forest (`contamination=0.1`) |
| Baseline period | Days 1–20 (training) |
| Detection period | Days 1–30 (inference) |

---

## 🔬 Why Isolation Forest?

- ✅ No labeled data needed — fully unsupervised
- ✅ Works well with high-dimensional behavioral features
- ✅ O(log n) inference — extremely fast at prediction time
- ✅ Naturally handles rare event detection
- ✅ Industry standard for anomaly detection tasks

---

## 🔮 Future Work

- [ ] Deep learning behavioral models (LSTM for sequence anomaly)
- [ ] Integration with enterprise SIEM platforms (Splunk, QRadar)
- [ ] Real-time streaming anomaly detection (Kafka + Flink)
- [ ] Graph-based insider threat analysis
- [ ] Gemini AI SOC analyst — natural language alert explanations
- [ ] Role-based access control for SOC team dashboard

---

## 🆚 Competitive Comparison

| Feature | ThreatWatch | Traditional SIEM | DLP Tools | UEBA Platforms |
|---|---|---|---|---|
| Behavioral Baseline Learning | ✅ Per-employee, 30-day | ❌ Static rules | ❌ Limited | ✅ But expensive |
| Unsupervised ML | ✅ Isolation Forest | ❌ Rule-based | ❌ Signature-based | ✅ Varies |
| Predictive Forecasting | ✅ 7-day regression | ❌ Reactive only | ❌ No forecast | ❌ Some products |
| Digital Twin Engine | ✅ Real vs predicted | ❌ Not available | ❌ Not available | ❌ Not standard |
| AI Natural Language Analyst | ✅ Gemini-powered | ❌ Not available | ❌ Not available | ⚠️ Emerging |
| Cost | ✅ **Free / Open-source** | ❌ $50k–$500k/yr | ❌ $20k–$300k/yr | ❌ Enterprise only |

---

## 👨‍💻 Project 

| Name | Enrollment No. | Branch |
|---|---|---|
| **Akshay Dhumda** | 246260316006 | Information Technology (SEM 4) |

**Institution:** Government Polytechnic Palanpur
**Cell:** SSIP Cell, GP Palanpur

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with ❤️ at Government Polytechnic Palanpur**
_"Application of knowledge is power" — New Palanpur for New India 4.0_

⭐ **Star this repo if ThreatWatch helped you!**

</div>

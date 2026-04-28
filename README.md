# PhishGuard: Hybrid Phishing Detection System

## Overview

PhishGuard is a real-time phishing detection system combining machine learning, threat intelligence, and LLM-based reasoning, deployed as a browser extension with a local backend.

It evaluates websites dynamically and assigns a risk score, enabling proactive detection of phishing attacks beyond traditional blacklist methods.

---

## Problem Statement

Modern phishing websites:
- mimic legitimate platforms (banks, UPI, login portals)
- use HTTPS and valid SSL certificates
- bypass blacklist-based security systems

As highlighted in the project pitch deck :contentReference[oaicite:0]{index=0}, existing systems fail against **zero-day phishing attacks**.

---

## Solution

PhishGuard performs **multi-layer analysis**:

1. URL structural analysis  
2. SSL & domain intelligence  
3. Threat intelligence lookup  
4. LLM-based contextual reasoning  

All combined into a **single risk score**.

---

## System Architecture

Browser Extension
↓
Content Script (URL capture)
↓
Background Script → Backend API (FastAPI)
↓
| 1. Structural ML Model |
| 2. SSL/Domain ML Model |
| 3. Threat Intel (URLScan API) |
| 4. LLM Analysis (Groq API) |
    ↓

Risk Scoring Engine
↓
Response → Extension UI


---

## Key Components

### 1. Browser Extension (Frontend)

- Monitors links in real-time
- Highlights risky URLs on hover :contentReference[oaicite:1]{index=1}  
- Blocks unsafe links before navigation
- Displays risk score in popup UI :contentReference[oaicite:2]{index=2}  

---

### 2. Backend API (FastAPI)

- Endpoint: `/analyze`
- Processes URLs and returns:
  - risk score
  - classification (Safe / Suspicious / Unsafe)
  - explanation

Core pipeline :contentReference[oaicite:3]{index=3}:
- Feature extraction
- Model inference
- API-based intelligence
- LLM reasoning
- Final scoring

---

### 3. Machine Learning Models

#### Structural Model
- Features:
  - URL length, dots, hyphens, digits, etc. :contentReference[oaicite:4]{index=4}  
- Model: Logistic Regression :contentReference[oaicite:5]{index=5}  

#### SSL / Domain Model
- Features:
  - domain age, DNS, WHOIS, HTTPS :contentReference[oaicite:6]{index=6}  
- Model: Logistic Regression :contentReference[oaicite:7]{index=7}  

---

### 4. Threat Intelligence Layer

- Uses URLScan API
- Detects known malicious domains :contentReference[oaicite:8]{index=8}  

---

### 5. LLM-Based Analysis

- Uses Groq API (LLaMA)
- Provides:
  - phishing likelihood
  - human-readable explanation :contentReference[oaicite:9]{index=9}  

---

### 6. Scoring Engine

Final score calculation :contentReference[oaicite:10]{index=10}:


Score = 0.35 * Structural + 0.15 * SSL + 0.5 * Threat Intel


Classification:
- Safe: 0 – 0.30  
- Suspicious: 0.30 – 0.65  
- Unsafe: > 0.65  

---

## Features

- Real-time phishing detection
- Multi-layer hybrid analysis
- Browser-level protection
- Local processing (privacy-first)
- Explainable AI outputs

---

## How to Run

### 1. Backend Setup


pip install fastapi uvicorn scikit-learn pandas numpy requests python-whois dnspython


Run backend:


uvicorn main:app --reload


---

### 2. Train Models


python train_structural_model.py
python train_ssl_model.py


---

### 3. Load Chrome Extension

- Open Chrome → Extensions → Developer Mode
- Load unpacked extension
- Select extension folder

---

## Example Workflow

1. User hovers over a link  
2. Extension sends URL for analysis  
3. Backend evaluates risk  
4. Link is:
   - highlighted (safe/suspicious/unsafe)
   - optionally blocked  

---

## Limitations

- Depends on external APIs (URLScan, LLM)
- Logistic Regression (basic model)
- Limited dataset scope
- No adversarial robustness

---

## Future Improvements

- Deep learning models (transformers)
- Real-time phishing dataset updates
- Browser-independent deployment
- Edge deployment (no backend)
- Advanced domain reputation systems

---

## Author

Ishaan Chand + Team

---

## License

For academic and research use
📄 requirements.txt
fastapi
uvicorn
pandas
numpy
scikit-learn
requests
python-whois
dnspython

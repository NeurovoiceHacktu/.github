# 

# NEUROVOICE
## Azure-Based Progressive AI Screening System
### Eraser Board – End-to-End Architecture Document
### 1st Runner Up - HackTU 7.0
---

## 1. PROBLEM CONTEXT
Parkinson’s Disease (PD) is a progressive neurological disorder where **speech and facial expression changes appear early**, often before clinical diagnosis. Traditional diagnosis is expensive, specialist-driven, and inaccessible at scale.

**Goal:**
Build a **non-diagnostic, ethical, scalable screening system** that:

- Uses **voice as the first signal**
- Escalates to **facial analysis only when required**
- Tracks **change over time**, not just one-time prediction
- Produces **explainable, clinician-ready outputs**
---

## 2. SOLUTION OVERVIEW (WHAT WE BUILT)
**NeuroVoice** is a **progressive, multimodal AI screening platform** deployed on **Microsoft Azure**, consisting of:

- **Two AI Levels**
    - Level 1: Voice-based screening (default)
    - Level 2: Facial expression analysis (conditional)

- **Two Dashboards**
    - User Dashboard (simple, reassuring)
    - Clinician Dashboard (detailed, explainable)

- **Azure-native, serverless architecture**
- **Explainable AI at every decision point**
---

## 3. HIGH-LEVEL ERASER FLOW
```
User Mobile App
      ↓
Consent & Onboarding
      ↓
Level 1: Voice Capture
      ↓
Voice AI (Azure ML)
      ↓
Risk + Explainability
      ↓
 ┌───────────────┐
 │               │
Low Risk     Medium / High Risk
 │               │
 ↓               ↓
User Trends   Level 2 Unlock
                 ↓
         Facial Expression Capture
                 ↓
         Facial AI (Azure ML)
                 ↓
         Combined Risk Engine
                 ↓
         Clinician Dashboard
```
---

## 4. ACTORS & INTERFACES
### Actor 1: User (Patient / Individual)
- Smartphone-based
- Daily voice recordings
- Optional facial video
- Sees trends, not diagnosis
### Actor 2: Clinician / Researcher
- Web dashboard
- Longitudinal tracking
- Explainable insights
- Exportable screening reports
---

## 5. LEVEL 1 — VOICE AI SCREENING (DEFAULT)
### Purpose
Detect **early speech deviations** associated with Parkinson’s risk using a low-friction method.

### Input
- 20–30 second guided speech task
- Works on any smartphone
- No camera required
### Azure Voice Pipeline
```
Audio Upload
   ↓
Azure Function (Quality Check)
   ↓
Feature Extraction
   ↓
Azure ML Voice Models
   ↓
Risk Score + Confidence
   ↓
SHAP Explainability
```
### Models Used (Ensemble)
- Feature-based model (Random Forest / Linear)
- Temporal model (LSTM / GRU)
- Spectrogram-based CNN
### Output
- Risk Category: Low / Medium / High
- Confidence (audio quality-aware)
- Feature-level explanations
---

## 6. LEVEL 2 — FACIAL EXPRESSION AI (CONDITIONAL)
### Trigger
- Activated **only if Level 1 risk ≥ threshold**
- Or explicit user consent
### Input
- Short selfie video (5–10 seconds)
### Azure Facial Pipeline
```
Video Upload
   ↓
Azure Function (Frame Extraction)
   ↓
Face Landmark Detection
   ↓
Temporal Facial Dynamics Model
   ↓
Facial Risk Score
```
### Features Analyzed
- Facial rigidity (hypomimia)
- Blink rate
- Mouth symmetry
- Micro-movement stability
### Key Design Choice
- Facial model is **independent** from voice model
- No forced multimodal fusion
---

## 7. MULTI-MODAL DECISION ENGINE
**Fusion occurs at decision level, not raw data level.**

```
Voice Risk Score
Facial Risk Score
Confidence Weights
        ↓
Final Screening Assessment
```
Benefits:

- Works even if one modality is missing
- Easier explainability
- Safer ethically
- More robust in real-world conditions
Implemented using **Azure Functions**.

---

## 8. DUAL DASHBOARD DESIGN
### A. USER DASHBOARD (Mobile)
**Objective:** Awareness, reassurance, continuity

Features:

- Daily risk indicator
- Trend vs personal baseline
- Simple explanations
- Privacy & consent controls
Example:

```
Status: Low Risk
Trend: Stable
Confidence: High
```
---

### B. CLINICIAN DASHBOARD (Web)
**Objective:** Clinical interpretability and monitoring

Features:

- Longitudinal timelines
- SHAP-based explanations
- Voice vs facial contribution split
- Exportable screening report (PDF)
Example Insights:

- Voice contribution: 65%
- Facial contribution: 35%
- Key drivers: pause duration, blink rate, pitch instability
---

## 9. AZURE SERVICE STACK
| Layer | Azure Service |
| ----- | ----- |
| API Gateway | Azure API Management |
| Serverless Logic | Azure Functions |
| ML Training & Inference | Azure Machine Learning |
| Media Storage | Azure Blob Storage |
| Feature Storage | Azure Data Lake Gen2 |
| Database | Azure Cosmos DB |
| Dashboards | Azure App Service |
| Authentication | Azure AD B2C |
| Monitoring | Azure Monitor + App Insights |
| Security | Azure Key Vault |
---

## 10. DATA GOVERNANCE & ETHICS
- Screening only (not diagnosis)
- Explicit uncertainty modeling
- Consent-based escalation
- Minimal raw data retention
- Feature-level storage preferred
- On-device + serverless hybrid processing
---

## 11. WHY THIS IS AN END-TO-END SOLUTION
✔ Progressive escalation
✔ Multimodal but modular
✔ Explainable by design
✔ Azure-native scalability
✔ Clinically usable outputs
✔ Ethically aligned with healthcare AI standards

---

## 12. ONE-LINE ERASER SUMMARY
> **“NeuroVoice is a progressive, Azure-based, explainable AI screening platform that uses voice as a first-line signal, conditionally escalates to facial analysis, and delivers dual dashboards for users and clinicians—without performing diagnosis.”**



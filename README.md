
**Topic 2: Clinical Decision Making and Pattern Recognition in Health Care**


---

## Concept

Hospital beds should be assigned by disease severity — not by how much money the hospital makes from a patient's insurance. This submission builds an AI system that scores patient vitals using the NEWS2 protocol (Royal College of Physicians, 2017) and a trained Random Forest classifier, then routes patients to the right bed type: ICU, Step-Down, General Ward, or Observation — ranked purely by clinical acuity.

---

## Deliverables

### 1. Written Report
**File:** `Acuity_First_Report_LeenaKatkar.docx`

2-page Word document covering:
- Concept Definition — what clinical decision-making AI is and why bed allocation matters
- The Past — Glasgow Coma Scale (1974), APACHE (1981), DRG payment incentives (1983)
- The Present — NEWS2, ML models on MIMIC-III data, documented racial bias in SOFA allocation
- The Future — agentic AI, continuous EHR monitoring, chain reasoning for transparency
- Opportunities & Threats for Cotiviti
- 3 Strategic Recommendations (ClinicalRoute AI product, Equity Monitoring Module, Agentic Pilot)
- 12 APA-formatted references

---

### 2. Hackathon POC Demo
**File:** `POC_AcuityBedAllocation.html`

Standalone HTML file — open directly in any browser, no server needed.

- 3 pre-loaded demo patients (Medicaid, Private PPO, Medicare) with different insurance types
- NEWS2 scoring computed live from 7 physiological parameters
- Priority queue sorts patients by clinical acuity score, not financial value
- Demonstrates the core concept visually: the Medicaid patient with the highest NEWS2 score ranks first

---

### 3. ML Project (Full Stack)
**File:** `ClinicalRouteAI.zip`

Flask + scikit-learn web application with a REST API backend.

**To run:**
```bash
unzip ClinicalRouteAI.zip
cd ClinicalRouteAI
pip install -r requirements.txt
python train_model.py    # generates model files (run once)
python app.py            # starts server at http://localhost:5000
```

**ML details:**
- Model: Random Forest Classifier — 200 estimators, max_depth=12
- Training: 12,000 synthetic patient records across 4 severity populations
- Validation: StratifiedKFold cross-validation (5 folds)
- Test accuracy: **92.67%** | CV accuracy: **92.85% ± 0.46%**
- Features: 8 physiological parameters (NEWS2 feature set)
- Output: 4 bed types — Observation / General Ward / Step-Down HDU / ICU

**What the UI shows:**
- Chain reasoning — step-by-step breakdown of each parameter and its NEWS2 points
- ML prediction with confidence % and probability distribution across all 4 classes
- Feature importances (top: Respiratory Rate 21.8%, Heart Rate 18.1%, SpO₂ 17.3%)
- Agreement/divergence flag between the ML model and the rule-based NEWS2 score
- Live priority queue — patients sorted by acuity, not payer type

**API endpoints:**
- `POST /api/assess` — accepts vitals JSON, returns full assessment
- `GET /api/model_info` — returns model accuracy, CV scores, feature importances

---

### 4. Presentation
**File:** `Acuity_First_Slides_LeenaKatkar.pptx`

9-slide deck (navy/blue palette) covering:
1. Title
2. The Problem — DRG incentive distortion
3. The Concept — acuity-first allocation
4. Past (1974–2012) — foundational scoring systems
5. Present — NEWS2, ML on EHR data, equity failures
6. Future — agentic AI and continuous monitoring
7. Live Demo — ClinicalRoute AI walkthrough
8. Strategic Recommendations for Cotiviti
9. Closing

---

### 5. Video Recording
*(Submitted separately as per assessment instructions)*

5-minute screen recording walking through the POC demo and ML application.

---

## File Summary

| File | Description |
|------|-------------|
| `Acuity_First_Report_LeenaKatkar.docx` | 2-page written report + APA bibliography |
| `POC_AcuityBedAllocation.html` | Standalone browser-based NEWS2 POC demo |
| `ClinicalRouteAI.zip` | Full Flask + scikit-learn ML project |
| `Acuity_First_Slides_LeenaKatkar.pptx` | 9-slide presentation deck |
| `README.md` | This file |

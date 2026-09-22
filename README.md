# PhishGuard — Fake Offer Letter & Phishing Inspector

**PhishGuard** is an AI-powered security analysis platform designed to detect fraudulent offer letters, check-cashing scams, equipment deposit traps, and employment phishing schemes. Combining deterministic rule-based heuristic checking with deep contextual reasoning via Large Language Models (LLMs), PhishGuard delivers explainable threat scores and real-time cybersecurity education.

---

## 📸 Key Features & Architecture Highlights

* **Dual-Layer Hybrid Scoring Engine:** Combines ultra-fast client-side heuristic pattern scanning with deep LLM semantic analysis.
* **Explainable AI (XAI) Reasoning:** Provides plain-language explanations detailing *why* an offer is flagged, breaking down social engineering tactics, urgency drivers, and financial red flags.
* **Calibrated Precision Framework:** Mitigates false positives by recognizing standard corporate HR protocols and accurately rating legitimate offers as low-risk (10–25%).
* **Educational Comparison Baseline:** Dynamically compares analyzed inputs against verified corporate hiring standards, transforming detection into active user awareness.
* **Instant Live Demo Mode:** Pre-loaded with verified scam, legitimate, and borderline test cases for immediate evaluation without manual input.
* **Zero-Dependency Single-Page Architecture:** Delivered as a standalone client-side web application built for minimal latency, high portability, and seamless deployment.

---

## 🛠️ Tech Stack & System Architecture

### Technical Stack

* **Frontend UI Framework:** HTML5, Tailwind CSS (via CDN), Lucide Icons
* **Data Visualization:** Custom SVG Radial Gauge System / Chart.js Rendering Engine
* **Logic Layer:** Asynchronous Vanilla JavaScript (ES6+)
* **AI Engine:** Google Gemini API (`gemini-2.5-flash` / REST Fetch Integration)
* **Design System:** Dark Mode Interface (Slate-900 palette, Glassmorphism accents, Emerald/Amber/Rose dynamic status gradients)

### System Flow

```
 ┌──────────────────────────────────────────────────────────────┐
 │                        User Input                            │
 │          (Offer Text & Optional Sender Email/URL)            │
 └──────────────────────────────┬───────────────────────────────┘
                                │
                                ▼
 ┌──────────────────────────────────────────────────────────────┐
 │             Module 2: Pure-JS Heuristic Engine               │
 │    • Evaluates weighted red flags (Upfront fees, domain    │
 │      mismatches, compensation ratio, urgency language)      │
 │    • Outputs: Raw Heuristic Score (0-100) + Rule Triggers     │
 └──────────────────────────────┬───────────────────────────────┘
                                │
                                ▼
 ┌──────────────────────────────────────────────────────────────┐
 │              Module 3: LLM Contextual Reasoning              │
 │    • Executes Gemini API request with structured JSON schema  │
 │    • Evaluates psychological manipulation & process norms    │
 │    • Outputs: Score Adjustment (-20 to +20) + Risk Factors   │
 └──────────────────────────────┬───────────────────────────────┘
                                │
                                ▼
 ┌──────────────────────────────────────────────────────────────┐
 │                 Hybrid Score Calculation                     │
 │      Final Score = Clamp(0, 100, Raw Heuristics + LLM Adj)   │
 │   • 0-30%: Low Risk  |  31-65%: Moderate  |  66-100%: High   │
 └──────────────────────────────┬───────────────────────────────┘
                                │
                                ▼
 ┌──────────────────────────────────────────────────────────────┐
 │              Module 5: Interactive Dashboard                 │
 │   • Animated Radial Gauge  • Executive Summary               │
 │   • Categorized Red Flags  • Legitimate Baseline Comparison  │
 └──────────────────────────────────────────────────────────────┘

```

---

## 🧩 Core System Modules

### Module 1: Input Interface & Preset Loader

Provides a high-density, structured interface featuring a text entry area with custom padding, optional domain/email entry fields, and instant 1-click test scenarios:

* **Scam Offer Preset:** Simulates an upfront check-cashing and equipment deposit fraud scheme.
* **Legitimate Offer Preset:** Simulates a standard tech industry offer letter using normal hiring processes.
* **Borderline Offer Preset:** Simulates an ambiguous remote listing with high compensation and low process visibility.

### Module 2: Local Heuristic Red Flag Engine

Executes synchronous client-side evaluation rules across weighted vectors:

* **Financial Transfer Requests (+25 Weight):** Scans for wire transfers, Zelle, Venmo, gift cards, and advance check purchases.
* **Coercive Urgency Drivers (+15 Weight):** Detects strict 24-hour response deadlines and pressure tactics.
* **Domain Mismatches (+20 Weight):** Identifies public domains (e.g., `@gmail.com`) claiming executive or corporate affiliation.
* **Unrealistic Pay-to-Effort Ratios (+10 Weight):** Highlights entry-level positions advertising outsized hourly compensation.
* **Process Omissions (+10 Weight):** Flags missing interview stages, lack of formal documentation, and vague job specifications.

### Module 3: LLM Analysis Engine

Dispatches the payload to the Gemini API utilizing a strict JSON output schema:

```json
{
  "llm_adjustment": 0,
  "overall_assessment": "Executive summary detailing overall document validity.",
  "risk_factors": [
    {
      "category": "Payment/Financial",
      "explanation": "Plain-language explanation of detected anomaly.",
      "severity": "high"
    }
  ],
  "missing_legitimate_elements": [
    "List of missing standard hiring elements."
  ]
}

```

*Fallback Safeguard:* In the event of API timeout, network failure, or unconfigured API keys, the system gracefully falls back to the deterministic heuristic score, maintaining uninterrupted system operational capability.

### Module 4: Sender & Domain Inspector

Extracts domain details from input headers to detect typosquatting patterns (e.g., character substitutions like `app1e.com`), unverified top-level domains, and discrepancies between corporate branding and email origins.

### Module 5: Analytics Dashboard

Renders an interactive threat evaluation screen upon scan completion:

1. **Threat Index Radial Gauge:** SVG element dynamically rendering the calculated percentage with corresponding color shifts (Green $\rightarrow$ Amber $\rightarrow$ Red).
2. **Executive Summary Card:** Presents LLM-synthesized narrative assessments.
3. **Categorized Risk Breakdown:** Grouped diagnostic tiles displaying severity badges (High, Medium, Low).
4. **Benchmark Comparison Grid:** Side-by-side comparative analysis matching user input attributes directly against standard corporate baselines.
5. **Mitigation Next Steps:** Actionable remediation guidance detailing reporting channels (FTC, IC3) and identity verification protocols.

---

## 🧪 Calibration Verification Matrix

| Test ID | Scenario Type | Expected Score | Primary Triggers |
| --- | --- | --- | --- |
| **Test Case A** | Obvious Fake (Equipment Deposit Scam) | **85% – 100%** (High Risk) | Advance payment requirement, non-standard payment networks (Zelle), extreme urgency. |
| **Test Case B** | Legitimate Offer (Standard Corporate) | **5% – 20%** (Low Risk) | Corporate domain match, formal onboarding portal reference, absence of financial requests. |
| **Test Case C** | Borderline Listing (Unvetted Remote Gig) | **40% – 55%** (Moderate) | High rate of compensation, lack of interview context, off-platform communications (Telegram). |

---

## 🚀 Getting Started

### Prerequisites

* A modern web browser (Google Chrome, Mozilla Firefox, Microsoft Edge, or Safari).
* An active Google Gemini API Key.

### Local Installation & Running

1. Clone the repository:
```bash
git clone https://github.com/your-username/phishguard.git
cd phishguard

```


2. Open `index.html` directly in your browser:
* **Linux/macOS:** `open index.html`
* **Windows:** `start index.html`


3. Enter your Gemini API key in the application settings modal within the interface to enable the hybrid LLM layer.

---

## 📂 Repository Structure

```
phishguard/
├── index.html        # Single-file HTML5 interface, Tailwind styling, and application logic
├── README.md         # Technical documentation and system specifications
└── LICENSE           # License agreement

```

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for further details.

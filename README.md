![1000008547](https://github.com/user-attachments/assets/9644233d-4a52-4df9-a732-9f974ee635d9)

# AXIOM — AI Certainty Middleware for Industrial Decision Systems

<!-- STATUS · VERSION · ARCHITECTURE -->
[![Status](https://img.shields.io/badge/STATUS-Development-F59E0B?style=flat-square)](https://github.com/AionSystem/AXIOM)
[![Version](https://img.shields.io/badge/version-v0.1.0-orange)](#)
[![Build](https://img.shields.io/badge/build-in--progress-yellow)](#)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)
[![Commercial License](https://img.shields.io/badge/Commercial-License%20Available-orange)](COMMERCIAL-LICENSE.md)
[![ORCID — Sheldon K. Salmon](https://img.shields.io/badge/ORCID-0009--0005--8057--5115-a6ce39?style=flat&logo=orcid&logoColor=white)](https://orcid.org/0009-0005-8057-5115)
[![DOI](https://zenodo.org/badge/1199929788.svg)](https://doi.org/10.5281/zenodo.19409945)

<!-- CORE ARCHITECTURE -->
[![CDI Engine](https://img.shields.io/badge/CDI_Engine-v0.1.0-4ade80?style=flat-square)](https://github.com/AionSystem/AXIOM)
[![AION Stack](https://img.shields.io/badge/AION-Constitutional_Stack-1976D2?style=flat-square)](https://github.com/AionSystem/AION-BRAIN)
[![STP](https://img.shields.io/badge/STP-Integrated-2E7D32?style=flat-square&logo=git&logoColor=white)](https://github.com/AionSystem/SOVEREIGN-TRACE-PROTOCOL)
[![Seal](https://img.shields.io/badge/Seal-SHA--256%20Bound-4527A0?style=flat-square&logo=hashnode&logoColor=white)](https://github.com/AionSystem/AXIOM)

<!-- TECH STACK -->
[![Made with Python](https://img.shields.io/badge/Made%20with-Python-3776AB?style=flat-square&logo=python&logoColor=white)](#)
[![FastAPI](https://img.shields.io/badge/API-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)](#)
[![Docker](https://img.shields.io/badge/Deploy-Docker-2496ED?style=flat-square&logo=docker&logoColor=white)](#)
[![Supabase](https://img.shields.io/badge/Storage-Supabase-3ECF8E?style=flat-square&logo=supabase&logoColor=white)](#)
[![Feedback Welcome](https://img.shields.io/badge/Feedback-welcome-brightgreen)](https://github.com/AionSystem/AXIOM/issues/new/choose)

> **Certainty infrastructure for industrial AI decisions.**
> NICE Challenge 2026 — AI & Communications | Yangtze Delta

---

## Table of Contents

- [Architect's Note on AI Use](#architects-note-on-ai-use)
- [Quick Start](#quick-start)
- [Repository Structure](#repository-structure)
- [Overview](#overview)
- [The CDI Engine](#the-cdi-engine)
- [AI Model Integration](#ai-model-integration)
- [NICE Challenge Alignment](#nice-challenge-alignment)
- [The AXIOM Ecosystem](#the-axiom-ecosystem)
- [Sovereign Trace Protocol Integration](#sovereign-trace-protocol-integration)
- [Technical Stack](#technical-stack)
- [Three Core Services](#three-core-services)
- [Data Security & Audit Integrity](#data-security--audit-integrity)
- [Installation & Deployment](#installation--deployment)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## Architect's Note on AI Use

AXIOM was designed, architected, and directed by Sheldon K. Salmon. AI tools (including large language models) were used as instruments — the same way a carpenter uses a saw. The intellectual core — the CDI Engine, the Confidence Deployment Index, the four scoring dimensions, the Uncertainty Mass architecture, the Epistemic Debt Score, the graduated model trust system, and the STP audit trail integration — is wholly human‑originated.

AXIOM is not a generative AI output. It is a human‑built reliability infrastructure layer, built on three years of independent research into certainty engineering for AI systems. Every formula, every threshold decision, and every architectural choice in the CDI Engine reflects human intent validated through systematic adversarial red-teaming.

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## Quick Start

Get the AXIOM CDI Engine running in under a minute.

```bash
git clone https://github.com/AionSystem/AXIOM.git
cd AXIOM
pip install -r requirements.txt
```

Score your first AI decision:

```python
from engine.cdi_engine import CDIEngine

engine = CDIEngine()
engine.register_model(
    model_id="your-model-id",
    calibration_status="UNCALIBRATED"
)

result = engine.score({
    "model_id": "your-model-id",
    "output_confidence": 0.82,
    "input_context": {"process": "quality_control", "line": "A3"},
    "timestamp": "2026-04-02T17:00:00Z"
})

print(result["cdi"])              # 0.71
print(result["validity_status"]) # VALID
print(result["um"])               # 0.28
print(result["action"])           # PROCEED
```

> **Note:** This runs the CDI Engine locally. The `api/` FastAPI server and Supabase sync are separate deployments and will not be active in local mode. All core CDI scoring and audit trail sealing work without them.

For the full API server and enterprise deployment, see [Installation & Deployment](#installation--deployment).

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## Repository Structure

> Key files for evaluators: `engine/cdi_engine.py` (scoring logic) · `engine/uncertainty_mass.py` (UM computation) · `engine/epistemic_debt.py` (EDS scoring) · `docs/cdi-formula.md` (CDI formula derivation) · `concept/NICE-PROPOSAL.md` (full NICE Challenge proposal)

```
AXIOM/
│
├── public/                         ← GitHub Pages landing page
│   ├── index.html                  ← AXIOM concept landing page
│   └── assets/                     ← Images, icons, diagrams
│
├── engine/                         ← CDI scoring engine (core)
│   ├── cdi_engine.py               ← CDI Engine v0.1.0 (scoring logic)
│   ├── uncertainty_mass.py         ← Uncertainty Mass (UM) computation
│   ├── epistemic_debt.py           ← Epistemic Debt Score (EDS) — 0–100 org metric
│   └── model_registry.py           ← AI model calibration registry + trust scoring
│
├── audit/                          ← Audit trail infrastructure
│   ├── stp_seal.py                 ← Sovereign Trace Protocol integration
│   └── audit_log.py                ← Decision log structure + export
│
├── connectors/                     ← Enterprise AI platform connectors
│   ├── openai_connector.py         ← OpenAI API connector
│   ├── anthropic_connector.py      ← Anthropic API connector
│   ├── generic_rest_connector.py   ← Generic REST API connector (any model)
│   └── README.md                   ← Connector documentation
│
├── api/                            ← REST API layer (FastAPI)
│   ├── server.py                   ← FastAPI server entry point
│   └── routes/
│       ├── score.py                ← POST /score — CDI scoring endpoint
│       ├── audit.py                ← GET /audit — audit trail retrieval
│       └── calibrate.py            ← POST /calibrate — model calibration update
│
├── dashboard/                      ← Web dashboard (optional)
│   ├── index.html                  ← CDI monitoring dashboard
│   └── assets/                     ← Dashboard assets
│
├── supabase/                       ← Database schema
│   └── schema.sql                  ← CDI scores, model registry, audit log tables
│
├── docs/                           ← Documentation
│   ├── cdi-formula.md              ← CDI formula derivation and weight rationale
│   ├── eds-formula.md              ← Epistemic Debt Score formula (5 components)
│   ├── architecture.md             ← System architecture and integration guide
│   └── deployment.md               ← Enterprise deployment guide
│
├── concept/                        ← Concept and proposal documentation
│   ├── NICE-PROPOSAL.md            ← NICE Challenge 2026 full proposal
│   ├── MARKET-ANALYSIS.md          ← Yangtze Delta industrial AI market analysis
│   └── USE-CASES.md                ← Industrial sector use cases
│
├── tests/                          ← Test suite
│   ├── test_cdi_engine.py          ← CDI scoring unit tests
│   ├── test_uncertainty_mass.py    ← UM computation tests
│   ├── test_eds.py                 ← EDS scoring tests
│   └── test_audit_trail.py         ← STP seal integration tests
│
├── AXIOM.md                        ← CDI Engine full technical documentation
├── NOTICE
├── COMMERCIAL-LICENSE.md
├── TEST_SUITE_AXIOM.md             ← Test suite documentation
├── NICE_PROPOSAL.md                ← NICE Challenge 2026 proposal (top-level copy)
├── LICENSE                         ← GPL-3.0
└── README.md                       ← This file
```

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## Overview

Most industrial AI deployments stop at the output. They compute, they score, they recommend — and then they hand an operator a decision with no way to know how much to trust it.

AXIOM is a model-agnostic middleware layer that sits between any deployed AI system and its downstream action triggers. Before a quality control model passes or rejects a component, before a predictive maintenance system flags or clears equipment, before a logistics optimizer routes or holds a shipment — AXIOM intercepts the AI output, scores its epistemic reliability with the Confidence Deployment Index (CDI), checks it against validated thresholds, and either certifies it for automated execution or gates it for human review. Every decision, every score, every gate is sealed to an immutable audit trail.

**How it works — three steps:**

1. An AI model produces an output with a confidence value. AXIOM's CDI Engine intercepts it, scores four reliability dimensions, and computes a CDI and Uncertainty Mass in real time.
2. An operator opens the monitoring dashboard and sees a reliability-weighted view of all AI decisions — green decisions are executing automatically, amber decisions are flagged for review, red decisions are blocked.
3. Every decision, every CDI score, and every audit event is permanently sealed with a cryptographic timestamp. If a decision is challenged, the sealed record proves exactly what the AI knew and how confident it was.

- [![GitHub](https://img.shields.io/badge/GitHub-AionSystem%2FAXIOM-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/AionSystem/AXIOM)
- [![AION Stack](https://img.shields.io/badge/Built%20on-AION%20Constitutional%20Stack-1976D2?style=flat-square)](https://github.com/AionSystem/AION-BRAIN)

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## The CDI Engine

The CDI Engine (v0.1.0) is the core of AXIOM — an epistemic scoring system that tells operators how much to trust each AI decision, and how much to trust the trust score itself.

### Scoring Dimensions

| Dimension | Weight | Description |
|-----------|--------|-------------|
| Output Confidence Score (OCS) | 35% | Model-declared confidence, adjusted for calibration history against verified ground truth |
| Corroboration Score (COR) | 30% | Agreement with recent historical decisions on comparable inputs within the same process context |
| Temporal Validity (TVR) | 20% | Model relevance decay since last calibration event or training update |
| Context Consistency (CCI) | 15% | Cross-check of input parameters against declared domain constraints and historical normal ranges |

> Weight rationale: OCS and COR carry the highest weight because they are the two externally-verifiable dimensions — model confidence can be calibrated against ground truth, corroboration requires independent decision history agreeing. TVR and CCI are internally-derived signals and are weighted accordingly. Full derivation: `docs/cdi-formula.md`

### CDI Formula

```
CDI = (OCS × 0.35) + (COR × 0.30) + (TVR × 0.20) + (CCI × 0.15)
UM  = 1 − min(calibration_coverage / 3, 1) × (1 − score_variance)
```

### Output

| CDI Range | Validity Status | Action |
|-----------|-----------------|--------|
| ≥ 0.70 | VALID | Decision executes automatically |
| 0.40–0.69 | DEGRADED | Decision flagged — human review required before execution |
| < 0.40 | SUSPENDED | Decision blocked — human authorization required |

### Uncertainty Mass (UM)

Every CDI score carries an Uncertainty Mass (UM) — a measure of how much the CDI score itself should be trusted:

| UM | Meaning |
|----|---------|
| < 0.35 | CDI is reliable — act on it |
| 0.35–0.60 | CDI is useful but uncertain — review before high-stakes actions |
| ≥ 0.60 | Do not rely on this CDI score |

> SUSPENDED decisions remain visible in the monitoring dashboard with a blocked status and human authorization prompt. They are never silently dropped — their presence is itself operational information.

### Graduated Model Trust

The CDI Engine does not assume any AI model is trustworthy without evidence. It uses a **graduated model trust score** [0.0–1.0] derived from calibration history against verified ground truth, which directly reduces the OCS uncertainty penalty as evidence accumulates.

| Trust Score | Calibration Status | OCS UM Penalty | Measurement Class |
|-------------|-------------------|----------------|-------------------|
| 0.0 | UNCALIBRATED (no ground truth) | 0.20 | INFERENTIAL |
| 0.01–0.59 | PARTIAL (1–49 validated decisions) | 0.08–0.20 | EVALUATIVE_PARTIAL |
| 0.60–0.85 | PARTIAL (50–249 validated decisions) | 0.03–0.08 | EVALUATIVE_PARTIAL |
| 1.0 | VERIFIED (formally calibrated) | 0.00 | EVALUATIVE_CERTIFIED |

The engine becomes more confident as evidence earns it — without requiring code changes. The trust score is declared at initialization, logged to the audit trail, and surfaced in every scored output. Call `engine.update_model_calibration(n, 'PARTIAL')` as ground truth accumulates.

### Epistemic Debt Score (EDS)

An organizational-level metric (0–100) measuring cumulative AI epistemic risk across all deployed systems:

| Component | Weight | What It Measures |
|-----------|--------|-----------------|
| Calibration Coverage | 25% | Proportion of deployed models with verified calibration |
| SUSPENDED Decision Rate | 25% | Rate of blocked decisions across all systems |
| DEGRADED Override Rate | 20% | Rate at which flagged decisions are manually overridden without review |
| Audit Trail Completeness | 20% | Proportion of decisions with sealed audit records |
| Model Age Distribution | 10% | Staleness of deployed models relative to calibration events |

> EDS > 80: AXIOM Certified — eligible for regulatory pre-clearance documentation.
> EDS 50–80: Active improvement required.
> EDS < 50: Systemic reliability risk — remediation engagement recommended.

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## AI Model Integration

AXIOM is model-agnostic. Any AI model that produces an output with a confidence value can be registered and scored by the CDI Engine. Built-in connectors are provided for common enterprise AI platforms.

### Connector Configuration

| Priority | Connector | Use Case |
|----------|-----------|----------|
| Primary | Generic REST (`generic_rest_connector.py`) | Any AI model with a REST API endpoint |
| Built-in | OpenAI Connector (`openai_connector.py`) | OpenAI API models (GPT series) |
| Built-in | Anthropic Connector (`anthropic_connector.py`) | Anthropic API models (Claude series) |

### How It Works

1. AI model produces output with confidence value → AXIOM connector intercepts it
2. CDI Engine scores OCS, COR, TVR, CCI across the four dimensions
3. CDI and UM are computed — VALID / DEGRADED / SUSPENDED gate fires
4. Decision sealed to STP audit trail with SHA-256 binding
5. If model calibration data available → `update_model_calibration()` called to reduce UM penalty without code changes

> The engine registers every model at initialization with a declared calibration status. New models start as UNCALIBRATED — the full UM penalty applies. As ground truth validation accumulates, calibration status upgrades automatically.

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## NICE Challenge Alignment

AXIOM was developed as the primary submission for the NICE Challenge 2026 — AI & Communications field. Full proposal: `concept/NICE-PROPOSAL.md`

| Requirement | Status |
|-------------|--------|
| Cutting-edge technical innovation — AI & Communications | ✅ |
| Independent IP rights | ✅ — DOI-registered foundation (AION Stack, CERTUS Engine) |
| Intention to establish entity — Yangtze Delta | ✅ |
| Detailed business plan — introduction through risk analysis | ✅ |
| Market analysis — Yangtze Delta industrial AI | ✅ |
| Financial and implementation plan (3-year) | ✅ |
| SWOT and risk analysis | ✅ |
| Project Manager introduction | ✅ — Sheldon K. Salmon, ORCID: 0009-0005-8057-5115 |
| Technology Readiness Level | TRL 5 — validated in relevant environment |
| Potential customers / partners in China | 🔄 In progress via NICE ecosystem |

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## The AXIOM Ecosystem

AXIOM is a unified platform with three core capabilities built into a single service offering:

| Service | Purpose | Access |
|---------|---------|--------|
| AI Decision Audit | One-time reliability assessment for deployed AI systems | Engagement-based |
| Continuous CDI Monitoring | Real-time per-decision scoring via middleware | License-based |
| Epistemic Debt Score Report | Quarterly organizational AI reliability report | Retainer-based |

All three share the same CDI Engine, the same UM architecture, and the same STP audit trail infrastructure.

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## Sovereign Trace Protocol Integration

AXIOM integrates with the Sovereign Trace Protocol — a permanence infrastructure with cryptographic sealing. Every CDI decision score, every UM value, every gate event, and every model calibration update is permanently sealed with a SHA-256 bound audit trail.

> **Audit integrity note:** Sealed records are filed to the STP ledger repository. This provides immutable timestamping — if a decision is challenged during a regulatory audit, quality review, or legal proceeding, the sealed record proves exactly what the AI knew, how confident it was, and whether uncertainty was properly flagged before the action triggered. The audit trail cannot be retroactively altered.

### How It Works

| Event | Trigger | Sealed Record |
|-------|---------|---------------|
| Decision Scored | Every CDI computation | CDI score, UM, validity status, model trust level, input context hash |
| Gate Fired | DEGRADED or SUSPENDED decision | Full decision context + gate reason + human review outcome |
| Calibration Updated | `update_model_calibration()` called | Old trust score, new trust score, sample count, timestamp |
| EDS Report Generated | Quarterly report cycle | Full EDS breakdown, all five components, organization identifier |

### Verification

Anyone can verify a sealed audit record by:

1. Recomputing the SHA-256 hash of the decision record
2. Comparing it to the hash sealed in the STP ledger
3. If they match, the record has not been altered since sealing

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## Technical Stack

| Layer | Technology | Why |
|-------|-----------|-----|
| CDI Engine | Python 3.11+ | Industrial-grade, enterprise-deployable, stdlib-compatible |
| API Layer | FastAPI | High-performance REST API, async-native, auto-documented |
| Model Registry | SQLite (dev) / PostgreSQL (prod) | Calibration history, trust scores, decision log |
| Audit Trail | Sovereign Trace Protocol + SHA-256 | Immutable, verifiable, tamper-evident |
| Connectors | Python REST clients | Model-agnostic, any AI platform |
| Dashboard | HTML + JavaScript | Lightweight, deployable anywhere |
| Backend Sync | Supabase (optional) | Real-time, row-level security |
| Deployment | Docker + GitHub Pages (`public/`) | Container-first, scalable, CDN-delivered landing page |
| License | GPL-3.0 with Commercial option | Open core for research, commercial for enterprise |

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## Three Core Services

### 🏭 AI Decision Audit — Enterprise Reliability Assessment

For a manufacturing enterprise that has deployed AI in production and needs to know how reliable those decisions actually are — without waiting for a failure to find out.

- CDI baseline scoring across all deployed AI decision systems
- Uncertainty Mass profiling per model, per process
- Epistemic Debt Score (EDS) organizational baseline (0–100)
- Sealed audit trail for every assessed decision
- Calibration gap identification — which models need ground truth validation
- Remediation roadmap with prioritized interventions
- Deliverable: CDI Baseline Report + EDS Report + sealed ledger entry

---

### 📊 Continuous CDI Monitoring — Real-Time Decision Scoring

For an enterprise that wants ongoing reliability scoring for every AI decision, automatically, without per-engagement consulting fees.

- AXIOM middleware deployed between AI model and action trigger
- CDI computed per decision in real time
- VALID / DEGRADED / SUSPENDED gates fire automatically
- Real-time monitoring dashboard with CDI distribution
- DEGRADED decisions routed to human review queue
- SUSPENDED decisions blocked pending human authorization
- Automatic model calibration updates as ground truth accumulates
- STP seal on every decision — continuous audit trail
- Monthly EDS report generated automatically

---

### 📜 Epistemic Debt Score — Organizational AI Reliability Report

For an executive team that needs to understand and report on the reliability of their organization's AI decision infrastructure — before regulators require it.

- Quarterly EDS report (0–100) across all deployed systems
- Five-component breakdown: calibration coverage, SUSPENDED rate, DEGRADED override rate, audit trail completeness, model age distribution
- Benchmark comparison against industry calibration datasets (accumulated from audit engagements)
- Regulatory compliance documentation package
- EDS improvement roadmap with quarterly milestone tracking
- AXIOM Certified status for organizations maintaining EDS > 80
- Sealed report — SHA-256 bound, tamper-evident, submittable to regulators

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## Data Security & Audit Integrity

- No personal data collected — AI decisions are scored by input context hash, not by individual identity
- Model outputs processed locally where possible — API-based models use encrypted transport (TLS 1.3)
- Calibration data stored with row-level security (Supabase RLS) when cloud sync is enabled
- Audit trail sealed with SHA-256 — tamper-evident, cannot be retroactively altered
- Enterprise deployments support air-gap operation — CDI Engine runs fully offline with local SQLite registry
- STP ledger entries are public-readable but write-authenticated — no unauthorized sealing
  > **Note:** Cloud infrastructure providers (Supabase, hosting platforms) may log request metadata per their own policies. Review their privacy documentation for deployment-level considerations.

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## Installation & Deployment

### 1. Clone the repo

```bash
git clone https://github.com/AionSystem/AXIOM.git
cd AXIOM
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Register your AI model

```python
from engine.cdi_engine import CDIEngine

engine = CDIEngine()
engine.register_model(
    model_id="your-model-id",
    model_type="rest",           # or "openai", "anthropic"
    calibration_status="UNCALIBRATED",
    calibration_samples=0,
    registered_by="your-deployment-id"
)
```

As ground truth validation accumulates, call `engine.update_model_calibration(n_samples, 'PARTIAL')` — no code changes required. The CDI Engine reduces the UM penalty automatically.

### 4. Configure Supabase (optional — for cloud sync and dashboard)

- Create a free Supabase project
- Run `supabase/schema.sql` to create the CDI scores, model registry, and audit log tables
- Set `SUPABASE_URL` and `SUPABASE_KEY` in your environment

### 5. Run the API server

```bash
uvicorn api.server:app --host 0.0.0.0 --port 8000
# POST /score   → CDI scoring endpoint
# GET  /audit   → Audit trail retrieval
# POST /calibrate → Model calibration update
```

### 6. Deploy with Docker

```bash
docker build -t axiom .
docker run -p 8000:8000 axiom
```

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## License

AXIOM is dual-licensed:

- **GNU General Public License v3.0** — for academic, research, and open-source use
- **Commercial License** — for enterprise deployment, proprietary integration, and OEM applications

| User Type | License |
|-----------|---------|
| Academic / Research | GPL-3.0 (Free) |
| Open-source projects | GPL-3.0 (Free) |
| Internal R&D (non-commercial) | GPL-3.0 (Free) |
| Enterprise deployment (commercial) | Commercial License (Fee) |
| OEM / white-label integration | Commercial License (Fee) |

See [`LICENSE`](LICENSE) for GPL terms and [`COMMERCIAL-LICENSE.md`](COMMERCIAL-LICENSE.md) for commercial licensing information.

For commercial licensing and enterprise engagement inquiries: [aionsystem@outlook.com](mailto:aionsystem@outlook.com)

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

## Acknowledgments

- AION Constitutional Stack — foundational certainty engineering frameworks
- CERTUS Engine — deployed precedent (VERITAS, UNDP Innocentive Challenge 2026)
- Sovereign Trace Protocol — cryptographic audit trail infrastructure
- FSVE (Formal Scoring and Validity Engine) — CDI scoring architecture origin
- FastAPI — API layer
- Supabase — optional cloud sync backend

[![↑ Back to Table of Contents](https://img.shields.io/badge/↑_Back_to-Table_of_Contents-374151?style=flat-square)](#table-of-contents)

---

> "The code is open source. The architecture is not replicable."

This is an application of the AION Constitutional Stack — applied to industrial AI decision systems and enterprise reliability infrastructure. The method travels. The judgment behind it doesn't.

---

CDI Engine v0.1.0 — NICE Challenge 2026 submission.
Epistemic Debt Score — organizational AI reliability, measured.
AXIOM — Every AI decision scored. Every gate sealed. Every audit trail permanent.

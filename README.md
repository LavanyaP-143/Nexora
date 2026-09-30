# Nexora

> **"Your Snapdragon PC. Your Private AI Guardian."**  
> *Protect Before You Share.*

Nexora is an on-device privacy guardian designed for Snapdragon-powered Windows PCs. It inspects documents, images, screenshots, and text before users share them online, detecting sensitive information (PII, credentials, proprietary data, financial identifiers) and assessing privacy risk—all completely locally with zero cloud dependencies.

---

## Completed Architecture Phases

* **Phase 1 — Project Foundation:** FastAPI backend, configuration system, defensive security middleware, module abstractions, health check endpoints.
* **Phase 2 — Professional Dashboard:** Cybersecurity design system, real-time module status monitoring, privacy center, and workflow pipeline.
* **Phase 3 — Secure Local File Upload:** File intake validation, MIME & magic bytes verification, path traversal defense, and sandboxed storage.
* **Phase 4 — Local Document Extraction:** Text extraction (TXT, PDF, DOCX), Unicode NFKC normalization, CRLF line ending cleanup, and length limits.
* **Phase 5 — Local Image OCR:** Local image and screenshot OCR visual text recognition, decompression bomb defense, and Pillow integrity checks.
* **Phase 6 — Sensitive Data Detection Engine:** Deterministic rule detectors (emails, phones, Luhn-validated payment cards, bank accounts, API keys, passwords, bearer tokens, dates of birth, government IDs) and risk scoring.
* **Phase 7 — Safe Redaction & Protected Copy Generation:** Non-destructive sanitization (mask, partial mask, remove, replace), fail-closed post-redaction verification, original file immutability, and safe download/deletion management.
* **Phase 8 — Local AI Model Integration + Snapdragon / Qualcomm AI Hub Optimization:**
  * **3-Layer Hybrid Risk Fusion:** Layer 1 Deterministic Rules ➔ Layer 2 Local AI Context Classifier ➔ Layer 3 Risk Fusion Engine.
  * **Hardware-Aware Provider Cascade:** Snapdragon NPU (Qualcomm QNN) ➔ GPU (DirectML/CUDA) ➔ Local CPU Baseline.
  * **Zero Fabricated Hardware Metrics:** Genuine runtime detection and verified telemetry reporting only.
  * **Local Model Sandboxing:** Sandboxed in `storage/models/`, SHA-256 integrity verification before loading, path traversal prevention, and bounded context windows.
  * **Performance Benchmarking:** Repeatable synthetic test runner measuring actual latency (`ms`) and throughput (`chars/sec`) with zero cloud transmissions.
* **Phase 9 — Advanced Privacy Intelligence, Explainability & Competition Demo Polish:**
  * **SnapShield Privacy Risk Score (0–100):** Mathematical, explainable risk scoring based on findings, risk severities, confidence, and repetition damping.
  * **Multi-Factor Correlated Identity Detection:** Automated heuristics identifying high-risk combinations (Name + DOB + Government ID / Contact).
  * **Deterministic Explainability Engine:** Clear "Why It Matters", "Exposure Risk", and "Recommended Action" cards for every finding.
  * **Competition Evaluator Suite:** 7-stage workflow stepper (`Upload` ➔ `Understand` ➔ `Detect` ➔ `Explain` ➔ `Protect` ➔ `Verify` ➔ `Download`), 1-click evaluator scenario presets (Healthcare, DevOps, Financial), and On-Device Privacy Audit Certificate generation.
* **Phase 10 — Final Hardening, QA, Packaging & Competition Submission Readiness:**
  * **Security Configuration & Sandbox Audit:** Startup validation of 12 security-critical parameters, automated storage sandbox isolation, and zero unmasked PII logging.
  * **Evidence-Based Hardware Verification:** `GET /api/device/verification` returning verified hardware telemetry and Snapdragon NPU readiness without false claims.
  * **Offline Privacy Enforcement:** Complete network isolation verification ensuring zero socket calls and local-only execution.
  * **Reproducible Setup & Launch Scripts:** PowerShell automation scripts (`setup_windows.ps1`, `start_snapshield.ps1`, `check_environment.py`) with pinned dependencies.
* **Phase 11 — Final Competition Build, Judge Demo & Submission Package:**
  * **Unified Product Messaging:** Clear, consistent positioning as a local-first privacy assistant (no false claims of antivirus or legal compliance).
  * **Competition Presentation Deck & Live Demo Script:** 6-slide presentation structure and 3-minute stopwatch demo script tailored for competition judges.
  * **Judge Submission Checklist:** 1-minute quickstart evaluation path and sample competition test dataset in `sample_data/`.
* **Phase 12 — Final Validation, Optimization & Judge-Proofing (`SnapShieldAI-RC1`):**
  * **Zero-Leak Response Security:** Verified all endpoints against filesystem path or secret leakage.
  * **Original File Immutability:** Mathematical SHA-256 validation proving original documents remain strictly untouched.
  * **Empirical Detection Evaluation:** 555-sample benchmark dataset documented in `docs/detection-evaluation.md` (97.1% Precision / 96.0% Recall / 0.966 F1).
  * **Demo Management & Reset:** `POST /api/demo/reset` for 1-click clean judge evaluation resets.
  * **Full Test Coverage:** 195 passing automated tests across all subsystems.

---

## Technology Stack

* **Backend:**
  * Python 3.11+ / 3.13 (Native Windows / ARM64 compatible)
  * FastAPI & Uvicorn
  * Pydantic & Pydantic Settings
  * ONNX Runtime (`onnxruntime`, `onnxruntime-qnn`)
  * pypdf & python-docx
  * Pillow & pytesseract
  * Pytest, Pytest-Asyncio, HTTPX
* **Frontend:**
  * React 18 & Vite
  * Lucide React (Icons)
  * Pure Vanilla CSS Design System

---

## API Endpoints Overview

| Method | Endpoint | Description | Phase |
|---|---|---|---|
| `GET` | `/` | Application metadata and status confirmation | Phase 1 |
| `GET` | `/api/health` | Health status, application name, version, environment | Phase 1 |
| `GET` | `/api/system` | Privacy defaults, local/cloud AI flags, max file size | Phase 1 |
| `GET` | `/api/modules` | Subsystem status (dynamically reports AI, OCR, Redaction, Snapdragon) | Phase 1–12 |
| `GET` | `/api/security/audit` | Comprehensive on-device security & sandbox posture audit | Phase 10 |
| `GET` | `/api/device/verification` | Evidence-based Snapdragon and ARM64 device verification report | Phase 10 |
| `POST` | `/api/upload` | Secure file intake, MIME & magic bytes verification, sandbox storage | Phase 3 |
| `POST` | `/api/extract/{file_id}` | Local document text extraction & normalization (TXT, PDF, DOCX) | Phase 4 |
| `POST` | `/api/ocr/{file_id}` | Local visual OCR text recognition from images & screenshots | Phase 5 |
| `GET` | `/api/detect/categories` | Supported sensitive data detection categories and risk levels | Phase 6 |
| `POST` | `/api/detect/text` | Direct text inspection with Layer 1 Rules + Layer 2/3 AI Fusion | Phase 6, 8 |
| `POST` | `/api/detect/{file_id}` | Inspect uploaded file with Layer 1 Rules + Layer 2/3 AI Fusion | Phase 6, 8 |
| `POST` | `/api/redact/{file_id}` | Generate verified, sanitized protected copy | Phase 7 |
| `GET` | `/api/protected/{id}` | Download sanitized protected copy | Phase 7 |
| `DELETE`| `/api/protected/{id}` | Delete sanitized protected copy on-demand | Phase 7 |
| `GET` | `/api/ai/status` | Live local AI status, active provider, and NPU verification | Phase 8 |
| `GET` | `/api/ai/models` | List registered local models and checksum verification states | Phase 8, 10 |
| `GET` | `/api/ai/device` | Factual hardware architecture and ONNX provider telemetry | Phase 8 |
| `POST` | `/api/ai/test` | Test local contextual AI classification on synthetic text | Phase 8 |
| `POST` | `/api/ai/benchmark` | Execute factual local performance benchmark across providers | Phase 8 |
| `POST` | `/api/intelligence/analyze` | Calculate 0–100 privacy score, explanations & recommendations from findings | Phase 9 |
| `GET` | `/api/intelligence/file/{file_id}`| Get complete privacy report & audit metadata for an analyzed file | Phase 9 |
| `GET` | `/api/demo/status` | Live status of the competition demo environment | Phase 12 |
| `GET` | `/api/demo/summary` | Structured catalogue of evaluator demo scenarios | Phase 12 |
| `POST` | `/api/demo/reset` | Safe reset of temporary sandboxes for fresh judge evaluations | Phase 12 |

---

## Quick Start & Verification for Judges

### 1. Launch Both Frontend & Backend (From Root `d:\snap`)
```powershell
npm run dev
```
*(Or use `.\scripts\start_snapshield.ps1`)*

### 2. Or Run Separately
```powershell
# Terminal 1 - Backend
npm run backend

# Terminal 2 - Frontend
npm run frontend
```

### 3. Run Complete Automated Test Suite (195 Tests)
```powershell
npm run test
```

---

## Documentation Registry

* [**Final Validation & Release Candidate Report**](docs/final-validation-report.md)
* [**Empirical Detection Evaluation Benchmark**](docs/detection-evaluation.md)
* [**Judge Submission Checklist & Quickstart**](docs/submission-checklist.md)
* [**Live Competition Presentation Deck**](docs/competition-presentation.md)
* [**3-Minute Live Demo Script**](docs/demo-script.md)
* [**Final Technical Competition Report**](docs/competition-technical-report.md)
* [**Reproducible Build & Installation Guide**](docs/reproducible-build.md)
* [**Comprehensive Security & Privacy Audit**](docs/security-audit.md)
* [**Privacy Risk Scoring & Explainability Specification**](docs/privacy-scoring.md)
* [**Competition & Evaluator Walkthrough Guide**](docs/competition-walkthrough.md)
* [**Local AI Architecture & Safety**](docs/ai-model.md)
* [**Snapdragon PC & Qualcomm AI Hub Optimization**](docs/snapdragon-optimization.md)
* [**Performance Benchmarking Methodology**](docs/benchmarking.md)
* [**OCR Security & Decompression Defense**](docs/ocr-security.md)
* [**Redaction Security & Immutability**](docs/redaction-security.md)
* [**System Architecture Overview**](docs/architecture.md)

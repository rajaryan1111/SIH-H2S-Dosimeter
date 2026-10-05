# H₂S Exposure Dosimeter Wristband

[![CI](https://github.com/rajaryan1111/SIH-H2S-Dosimeter/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/rajaryan1111/SIH-H2S-Dosimeter/actions/workflows/ci.yml)

**SIH 2026 · SIH26118 · Hardware + Software**

A low-cost **passive colorimetric H₂S exposure-dosimeter wristband** paired with computer vision and ML to estimate cumulative hydrogen-sulfide exposure from a photographed chemical strip.

## The problem

H₂S exposure can be difficult to monitor continuously with low-cost wearable hardware. This project explores a disposable visual dosimeter whose color changes with cumulative exposure and can be read by a phone.

## How it works

```text
H₂S exposure
     │
     ▼
Copper-acetate colorimetric strip
     │  progressive color change
     ▼
Phone camera + reference color card
     │
     ▼
ROI detection → color correction → CIE Lab / ΔE2000
     │
     ▼
ML regression → estimated cumulative dose (ppm·hr)
     │
     ▼
FastAPI → alerts / history / reports
     │
     ▼
React dashboard
```

## Engineering highlights

### Computer vision + colour science

- Region-of-interest detection for the chemical strip and reference card.
- sRGB → CIE XYZ → CIE L\*a\*b\* conversion.
- CIE ΔE2000 perceptual colour-difference calculation.
- Reference-card based lighting correction.

### Machine learning

- Regression pipeline for cumulative-dose estimation.
- Model training/evaluation utilities and feature analysis.
- Synthetic/physics-based data is currently used for model development.

### Backend

- FastAPI REST API.
- SQLAlchemy data layer.
- JWT-based authentication and role checks.
- Worker, reading, alert and reporting workflows.
- PDF report generation.

### Dashboard

- React + Vite.
- Worker overview, readings, alerts and reports.
- Authenticated API client with environment-based backend configuration.

## Current implementation status

| Component | Status |
|---|---|
| Colour-science / ML pipeline | ✅ Implemented |
| FastAPI backend | ✅ Implemented |
| Admin dashboard | ✅ Implemented |
| Automated backend/offline checks | ✅ 49 API tests + 16 offline checks documented |
| Flutter mobile client | 🚧 Not implemented |
| Real-world chemical-strip dataset | 🚧 Required for real validation |

### Important limitation

The current ML evaluation is **not a real-world accuracy claim**. The training/evaluation workflow uses synthetic or physics-based data because a sufficiently large labelled dataset of real H₂S-exposed strips has not yet been collected. Real-hardware validation is therefore an explicit next step.

## Safety / scope

This is a research and prototype project. It should **not** be used as a certified occupational-safety instrument. Any real deployment would require controlled chemical validation, calibration, environmental testing, sensor/strip characterization and appropriate regulatory review.

## Repository structure

```text
software/
├── ml_pipeline/     colour processing, dataset creation, regression and evaluation
├── backend/         FastAPI, SQLAlchemy, auth, readings, alerts and reports
└── dashboard/       React/Vite admin interface
```

Generated datasets, trained models, plots, databases and frontend build output are excluded from version control.

## Run locally

### Backend

```bash
cd software/backend
pip install -r requirements.txt
cp .env.example .env
uvicorn main:app --reload
```

Swagger UI is available at `/docs` while the server is running.

### Dashboard

```bash
cd software/dashboard
npm install
cp .env.example .env
npm run dev
```

### ML pipeline

```bash
cd software/ml_pipeline
pip install -r requirements.txt
python image_processor.py
python demo_simulator.py
python model_evaluator.py
```

## Testing

Backend tests cover authentication/authorization, workers, readings, alerts, dashboard aggregation and reporting. Offline checks can run without a live backend; API integration tests exercise the running service.

## Tech stack

**Python · FastAPI · SQLAlchemy · PostgreSQL/SQLite · JWT · OpenCV · CIE colour science · scikit-learn · React · Vite · Chart.js · pytest**

## Author

Built by **Raj Aryan** and the SIH project team as a hardware/AI engineering prototype.

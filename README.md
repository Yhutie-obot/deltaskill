# DeltaSkill

**AI-Powered Vocational Skills & Adaptive Learning Platform for Niger Delta Youth**

> Project Code: DS-2026-001  
> Category: ML Engineering / EduTech / MLOps  

## 1. Project Overview

DeltaSkill is an AI-powered EduTech platform designed to provide adaptive, culturally relevant vocational and entrepreneurial skills training to young people across the South-South geopolitical zone of Nigeria.

The platform is designed around a central idea: learning should adapt to the learner. Instead of providing every learner with the same fixed learning path, DeltaSkill uses machine learning to analyse learner behaviour, predict dropout risk, recommend relevant learning content, and provide actionable analytics to instructors.

The target region includes Delta, Rivers, Bayelsa, Akwa Ibom, Cross River, Edo, and Ondo States.

## 2. Problem Statement

The project addresses several connected challenges affecting youth in the Niger Delta:

- Environmental degradation has disrupted traditional livelihoods such as farming and fishing.
- Youth unemployment and skill mismatch limit access to sustainable economic opportunities.
- Economic pressure contributes to education dropout.
- Traditional vocational programmes often use one-size-fits-all learning paths.
- Remote communities face connectivity and geographic barriers.
- Instructors often lack timely analytics about learner progress and dropout risk.

DeltaSkill therefore aims to make vocational learning adaptive, accessible, data-driven, and relevant to the local context.

## 3. Project Objectives

DeltaSkill must:

1. Predict learner success and dropout risk early.
2. Dynamically adapt learning paths based on learner performance and engagement.
3. Recommend appropriate modules and content formats for individual learners.
4. Provide personalised feedback and automated interventions.
5. Give instructors and community facilitators actionable learner and regional analytics.
6. Support Standard English and key Nigerian Pidgin instructional/interface content.
7. Operate as a reproducible, containerised ML application.

## 4. Core Platform Features

### 4.1 Adaptive Learning Engine

The adaptive learning engine is the primary ML challenge. It analyses learner behaviour and updates learner skill profiles using signals such as quiz performance, engagement, and time-on-task.

It should:

- Route struggling learners to remedial content.
- Accelerate strong learners.
- Recommend learning sequence and difficulty.
- Support video, text, quizzes, and audio content.
- Use a model-driven approach rather than a simple rule-based system.

### 4.2 Learner Success & Dropout Risk Predictor

A supervised ML model will estimate the probability that an enrolled learner will fail to complete a course.

The system should:

- Run predictions at defined checkpoints.
- Produce an `At-Risk` or `On-Track` class.
- Produce a calibrated probability score.
- Trigger instructor alerts when risk exceeds the selected threshold.

### 4.3 Smart Content Recommendation Engine

The recommendation system will recommend the next valuable module or learning resource.

Required approaches:

- Collaborative filtering.
- Content-based filtering.
- Hybrid recommendation using both signals.

Optional bonus:

- Contextual bandit/reinforcement-learning framing.

### 4.4 Progress Tracking & Digital Certification

The platform should provide:

- Learner completion percentage.
- Quiz scores.
- Skill badges.
- Recommended next steps.
- Course completion certificates as PDF.
- Instructor-level cohort progress summaries.

### 4.5 Regional Analytics Dashboard

Grafana dashboards should provide regional analytics including:

- Skill distribution across the seven target states.
- Dropout trends by LGA.
- Dropout trends by age group.
- Dropout trends by device type.
- Model accuracy/performance.
- Inference latency.
- Data drift indicators.

### 4.6 Multilingual Support

The application must support Standard English for user-facing content.

Key instructional audio and interface labels should support Nigerian Pidgin English. The architecture should be extensible to Ijaw, Itsekiri, and Efik in future versions.

## 5. Machine Learning Tasks

### Task 1: Student Performance & Dropout Risk Prediction

The model predicts dropout probability or projected completion performance from learner engagement history.

#### Minimum Feature Space

The dataset/model should include:

- Time spent per module.
- Quiz attempt count and scores per module.
- Clickstream density.
- Video completion rate.
- Days since last login.
- Module sequence position at dropout/completion.
- Learner state/LGA.
- Age group.
- Highest education level.
- Primary device type.
- Connectivity tier.
- Skill domain enrolled.

#### Required Model Experiments

All of the following must be trained, evaluated, and logged:

1. Logistic Regression.
2. Random Forest Classifier.
3. XGBoost.
4. LightGBM.
5. CatBoost.
6. Neural Network using MLP or LSTM.
7. An ensemble/stacking approach combining at least two models.

No required algorithm should be skipped.

#### Required Evaluation

For each model, report:

- AUC-ROC.
- Weighted F1.
- Macro F1.
- Precision at threshold 0.5.
- Recall at threshold 0.5.
- Precision at an optimised threshold.
- Recall at an optimised threshold.
- Calibration curve.

For the final selected model:

- SHAP feature importance/summary analysis.

Because dropout is an imbalanced classification problem, class imbalance must be addressed and the chosen method justified.

### Task 2: Adaptive Content Recommendation

The recommendation system should recommend the next module/content type using the learner's current state.

Required approaches:

- Collaborative filtering.
- Content-based filtering.
- Hybrid model.

Optional:

- Contextual bandit.

#### Recommendation Evaluation

Offline metrics:

- Precision@3 and Precision@5.
- Recall@3 and Recall@5.
- NDCG@3 and NDCG@5.

Simulated online metrics:

- Click-through-rate proxy.
- Module completion rate after recommendation.

## 6. Data Requirements

The project requires a reproducible synthetic dataset representing the South-South Nigerian EduTech context.

Minimum requirements:

| Requirement | Target |
|---|---:|
| Learner-course interaction rows | 10,000+ |
| Unique learner profiles | 2,000+ |
| Modules per course | 8+ |
| Courses | 5+ |
| States | 7 |
| Dropout rate | 25–35% |
| English interactions | 60% |
| Pidgin-interface interactions | 40% |
| Mobile devices | 65% |
| Desktop devices | 25% |
| Tablet devices | 10% |
| Activity period | 12 months |

The seven states are Delta, Rivers, Bayelsa, Akwa Ibom, Cross River, Edo, and Ondo.

The synthetic data should be generated with Python using NumPy, pandas, and Faker. Random seeds must be explicitly set so that generation is reproducible.

## 7. Technology Stack

The project specification requires the following stack:

### Machine Learning & Experiment Tracking

- Python 3.11+
- scikit-learn
- XGBoost
- LightGBM
- CatBoost
- PyTorch
- SHAP
- MLflow 2.x

### Backend

- FastAPI
- Python

### Frontend

- TypeScript
- React
- Next.js 14+

### Database

- PostgreSQL

### Caching / Queue

- Redis (optional but recommended)

### Infrastructure

- Docker
- Docker Compose

### Deployment

- Railway

### Monitoring

- Prometheus
- Grafana

### Version Control

- Git
- GitHub

### Model Tracking

- MLflow Tracking Server
- MLflow Model Registry

## 8. System Architecture

The intended architecture is a containerised monorepo containing:

```text
                        ┌──────────────────────┐
                        │      Next.js UI      │
                        │   Learner/Instructor │
                        └──────────┬───────────┘
                                   │
                                   ▼
                        ┌──────────────────────┐
                        │      FastAPI API     │
                        │ Business + ML APIs   │
                        └───────┬───────┬──────┘
                                │       │
                 ┌──────────────┘       └──────────────┐
                 ▼                                      ▼
        ┌────────────────┐                     ┌────────────────┐
        │  PostgreSQL    │                     │     Redis      │
        │ Learner/Data   │                     │ Cache/Queue    │
        └────────────────┘                     └────────────────┘
                 │
                 ▼
        ┌──────────────────────┐
        │ ML Prediction &      │
        │ Recommendation Layer │
        └──────────┬───────────┘
                   │
          ┌────────┴─────────┐
          ▼                  ▼
   ┌────────────┐     ┌─────────────┐
   │   MLflow   │     │ Prometheus  │
   │ Tracking + │     │  Metrics    │
   │ Registry   │     └──────┬──────┘
   └────────────┘            ▼
                       ┌────────────┐
                       │  Grafana   │
                       │ Dashboards │
                       └────────────┘
```

All services must be orchestrated by Docker Compose.

## 9. Repository Structure

The repository will follow the required monorepo structure:

```text
deltaskill/
├── backend/
│   ├── app/
│   ├── tests/
│   └── requirements.txt
├── frontend/
│   ├── app/
│   ├── components/
│   └── package.json
├── ml/
│   ├── data/
│   ├── notebooks/
│   ├── src/
│   ├── models/
│   └── experiments/
├── infra/
│   ├── prometheus/
│   ├── grafana/
│   └── mlflow/
├── docs/
│   ├── architecture/
│   ├── decisions/
│   └── reports/
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

## 10. MLflow Requirements

MLflow is mandatory.

Every experiment, including failed experiments, must be logged.

Each run should capture at minimum:

- Hyperparameters.
- Required evaluation metrics.
- Confusion matrix artifact.
- SHAP summary artifact where applicable.
- Training data schema.
- Feature names.
- Data types.
- Dataset shape.
- Python version.
- Library/environment versions.
- `requirements.txt` as an artifact.

The final selected model for each ML task must be registered in the MLflow Model Registry and promoted through:

```text
staging → production
```

## 11. Docker Compose Requirement

The root `docker-compose.yml` must orchestrate:

- FastAPI backend.
- Next.js frontend.
- PostgreSQL.
- MLflow Tracking Server.
- Prometheus.
- Grafana.
- Redis where used.

The evaluator should be able to run:

```bash
docker-compose up --build
```

from the repository root and access the services through their defined ports without manual service setup.

## 12. Development Roadmap

### Phase 1 — Foundations & Data

- Create GitHub repository.
- Create monorepo structure.
- Create Docker Compose skeleton.
- Build reproducible synthetic dataset.
- Perform EDA.
- Document data schema.
- Run MLflow locally.

### Phase 2 — ML Experimentation

- Train all seven required model approaches.
- Log every experiment to MLflow.
- Compare model performance.
- Perform SHAP analysis.
- Select and justify final model.
- Build the FastAPI risk prediction endpoint.

### Phase 3 — Platform Build

- Build recommendation engine.
- Build learner dashboard.
- Build instructor dashboard.
- Create PostgreSQL schema and migrations.
- Build Grafana regional analytics.
- Integrate the services through Docker Compose.

### Phase 4 — Deployment & Polish

- Deploy to Railway.
- Configure Prometheus.
- Build Grafana dashboards.
- Complete ML experimentation report.
- Finalise README.
- Prepare presentation and live demo.

## 13. Final Deliverables

### GitHub Repository — 30%

The repository must include:

- Clean monorepo structure.
- Comprehensive README.
- Docker Compose configuration.
- Backend requirements.
- Frontend package configuration.
- Reproducible synthetic data generation.
- `.env.example`.
- Meaningfully documented code.

### ML Experimentation Report — 35%

Minimum 15-page PDF containing:

- Executive summary.
- Problem framing.
- Dataset generation.
- Feature engineering.
- Class imbalance handling.
- Complete experiment log.
- Model selection justification.
- SHAP analysis.
- Failure analysis.
- Future work.

### Live Deployment — 20%

- Public Railway URL.
- Functional core features.
- Accessible MLflow UI.
- Grafana dashboard showing live metrics.

### Presentation & Demo — 15%

- Maximum 20 slides.
- 15-minute presentation.
- Live platform demonstration.
- Real-world impact narrative.
- Proposed pilot with a local NGO, vocational centre, or NYSC programme.

## 14. Evaluation & Pass Criteria

The grading weights are:

| Criterion | Weight |
|---|---:|
| GitHub Repository Quality | 30% |
| ML Experimentation Report | 35% |
| Live Railway Deployment | 20% |
| Final Presentation & Demo | 15% |

A pass requires:

- All seven algorithm experiments logged in MLflow.
- Functional Railway deployment.
- ML report submitted.

Distinction additionally requires:

- Contextual SHAP interpretation specific to the Niger Delta.
- At least one bonus feature.
- Failure analysis in the final report.

## 15. Academic Integrity

This is an individual project.

AI-assisted tools may be used as productivity aids, but the student must understand and be able to explain the code and ML decisions. The ML experimentation and report must not simply be wholesale generated from templates or copied.

External datasets must be properly cited with source, licence, and access date.

## 16. Local Development

### Prerequisites

Install:

- Git
- Docker Desktop
- Python 3.11+
- Node.js
- npm
- A GitHub account

### Clone the repository

```bash
git clone <YOUR_PUBLIC_GITHUB_REPOSITORY_URL>
cd deltaskill
```

### Start the application

```bash
docker-compose up --build
```

Service ports will be documented here as they are finalised.

## 17. Environment Variables

Secrets must never be committed to GitHub.

Copy the example environment file:

```bash
cp .env.example .env
```

Add local credentials and service configuration to `.env`.

## 18. Reproducibility

The dataset generation process must use explicit random seeds.

All experiments should record their parameters, metrics, environment, and artifacts in MLflow.

The goal is for another developer or examiner to reproduce the major project results from the repository.

## 19. Monitoring

Prometheus will collect application and model-serving metrics.

Grafana will visualise:

- Learner activity.
- Dropout trends.
- Model performance.
- Prediction latency.
- Regional skill distribution.
- Data drift indicators.

## 20. Deployment

The target deployment platform is Railway.

The deployed application should expose the core platform functionality and monitoring/tracking interfaces required by the project specification.

Deployment instructions will be expanded as the infrastructure configuration is implemented.

## 21. Project Status

**Current stage:** Repository and project documentation setup.

Planned immediate tasks:

- [ ] Create public GitHub repository.
- [ ] Clone repository locally.
- [ ] Add comprehensive README.
- [ ] Create initial monorepo directories.
- [ ] Add `.gitignore`.
- [ ] Add `.env.example`.
- [ ] Create initial Docker Compose skeleton.
- [ ] Build synthetic dataset generator.
- [ ] Set up MLflow.
- [ ] Begin EDA and ML experimentation.

## 22. Reference

This README is based on the DeltaSkill AI/ML Capstone Project Brief, Project Code **DS-2026-001**.

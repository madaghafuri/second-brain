---
title: MLOps Learning Roadmap
created: 2026-07-13
tags:
  - project
  - mlops
  - learning
status: active
source_path: /home/mada/side_projects/second-brain
---

# MLOps Learning Roadmap

## Outcome

Build the skills and portfolio to design, build, and maintain production ML systems end-to-end: from experiment tracking and pipelines to deployment, monitoring, and retraining.

## Context

- Background: software engineer (polyglot: Go, Python, Java)
- Commitment: ~10-15 hours/week over 24 weeks
- Related map: [[mlops]]
- Prerequisites: comfortable with Python, Docker, Git, CI/CD concepts

## Timeline Overview

| Phase | Topic | Duration |
|-------|-------|----------|
| 1 | ML Fundamentals | Weeks 1-4 |
| 2 | Experimentation & Reproducibility | Weeks 5-7 |
| 3 | ML Pipelines & Orchestration | Weeks 8-10 |
| 4 | Model Serving & Deployment | Weeks 11-14 |
| 5 | CI/CD for ML | Weeks 15-17 |
| 6 | Monitoring & Observability | Weeks 18-20 |
| 7 | Advanced Topics & Capstone | Weeks 21-24 |

---

## Phase 1: ML Fundamentals (Weeks 1-4)

**Goal**: Understand the ML model lifecycle end-to-end. Be able to train, evaluate, and serve a basic model.

### Topics
- Supervised vs unsupervised learning, train/val/test split, overfitting
- Common model types: linear regression, decision trees, random forests, gradient boosting
- Feature engineering basics, handling missing data, categorical encoding
- Evaluation metrics: accuracy, precision, recall, F1, ROC-AUC, RMSE, MAE
- Serving a model with a REST API (FastAPI)

### Materials
- [Kaggle Learn](https://www.kaggle.com/learn) - Intro to Machine Learning
- [Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow](https://www.oreilly.com/library/view/hands-on-machine-learning/9781098125967/) (Géron) - Chapters 1-4
- FastAPI docs: simple model serving endpoint

### Assignment
Build a house-price prediction API:
1. Train a regression model on the [Ames Housing dataset](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques)
2. Expose a `/predict` endpoint via FastAPI that accepts house features and returns a price
3. Containerize with Docker

### Checkpoint deliverables
- `train.py` that trains and saves a model
- `app.py` with FastAPI POST `/predict`
- `Dockerfile` and `docker-compose.yml`
- `requirements.txt`
- `README.md` with run instructions

---

## Phase 2: Experimentation & Reproducibility (Weeks 5-7)

**Goal**: Track experiments, version data and models, and make any result reproducible.

### Topics
- Experiment tracking: MLflow, Weights & Biases
- Data versioning: DVC (Data Version Control)
- Environment reproducibility: Docker + Docker Compose, Conda
- Model registry: MLflow Model Registry
- Configuration management: Hydra, pydantic-settings

### Materials
- [MLflow docs: Tracking](https://mlflow.org/docs/latest/tracking.html)
- [DVC getting started](https://dvc.org/doc/start)
- [Made With ML](https://madewithml.com/) - MLOps section

### Assignment
Add experiment tracking and data versioning to your Phase 1 project:
1. Use MLflow to log all training runs (parameters, metrics, model artifacts)
2. Use DVC to version the training dataset
3. Create a `config.yaml` using Hydra for all training hyperparameters
4. Register the best model in MLflow Model Registry
5. Demonstrate that a teammate can reproduce a specific run

---

## Phase 3: ML Pipelines & Orchestration (Weeks 8-10)

**Goal**: Automate the ML workflow into reusable, scheduled pipelines.

### Topics
- Pipeline concepts: data ingestion → validation → preprocessing → training → evaluation → deployment
- Orchestration: Prefect, Airflow, Kubeflow Pipelines
- Feature stores (conceptual): Feast
- Data validation: Great Expectations, Pandera

### Materials
- [Prefect docs: ML workflows](https://docs.prefect.io/latest/tutorials/ml-workflows/)
- [Kubeflow Pipelines docs](https://www.kubeflow.org/docs/components/pipelines/)
- [Great Expectations docs](https://docs.greatexpectations.io/docs/)

### Assignment
Build a feature pipeline + training pipeline:
1. Ingest raw data, validate schema with Great Expectations
2. Run feature engineering (as a Prefect flow)
3. Run training (as a downstream Prefect flow)
4. Store features using Feast (local mode) or a simple Parquet-based feature store
5. Containerize all pipeline steps

---

## Phase 4: Model Serving & Deployment (Weeks 11-14)

**Goal**: Deploy models to production with proper serving patterns, scaling, and rollback.

### Topics
- Serving patterns: REST, gRPC, batch inference, streaming
- Serving frameworks: BentoML, Ray Serve, MLflow Serving
- Container orchestration: Kubernetes (K8s) basics for ML
- Model optimization: ONNX, TorchScript, TensorRT
- Canary deployments, blue/green deployments
- Serverless ML: AWS SageMaker, GCP Vertex AI (basics)

### Materials
- [BentoML docs](https://docs.bentoml.com/en/latest/)
- [Kubernetes in Action](https://www.manning.com/books/kubernetes-in-action) (or [K8s for ML](https://mlinproduction.com/kubernetes-for-ml-part-1/))
- [ONNX tutorials](https://github.com/onnx/tutorials)

### Assignment
Production-grade model serving:
1. Package your model with BentoML
2. Create a Docker image that serves the model via gRPC and REST
3. Deploy to a local K8s cluster (minikube or kind) with 2 replicas
4. Export the model to ONNX and benchmark latency vs native
5. Implement a canary deployment strategy (route 10% traffic to new version)

---

## Phase 5: CI/CD for ML (Weeks 15-17)

**Goal**: Automate testing, validation, and deployment of ML pipelines.

### Topics
- ML pipeline CI/CD: GitHub Actions, GitLab CI
- Model testing: validation sets, slice-based evaluation, data tests
- Infrastructure as Code: Terraform (for ML infra), Helm (for K8s)
- A/B testing and experiment design for ML
- Feature stores in CI/CD

### Materials
- [Effective Testing for ML Systems](https://www.jeremyjordan.me/testing-ml/) (Jeremy Jordan)
- [Terraform: Getting Started](https://developer.hashicorp.com/terraform/tutorials)
- GitHub Actions docs

### Assignment
CI/CD pipeline for your ML project:
1. GitHub Actions workflow that runs on PR:
   - Lint code, run unit tests
   - Train on a small data slice
   - Validate model quality vs baseline
   - Run Great Expectations data validation
2. On merge to main:
   - Train full model
   - Register model in MLflow
   - Deploy to staging (K8s)
3. Manual approval gate for production rollout

---

## Phase 6: Monitoring & Observability (Weeks 18-20)

**Goal**: Detect model degradation in production and trigger retraining.

### Topics
- Data drift vs concept drift vs model decay
- Monitoring tools: Evidently AI, WhyLabs, Prometheus + Grafana
- Logging and tracing: MLflow (model events), structured logging
- Automated retraining triggers
- Dashboarding for ML stakeholders

### Materials
- [Evidently AI docs](https://docs.evidentlyai.com/)
- [Monitoring ML Models in Production](https://christophergs.com/machine%20learning/2020/03/14/how-to-monitor-machine-learning-models/) (blog)
- [Prometheus docs](https://prometheus.io/docs/introduction/overview/)

### Assignment
End-to-end monitoring:
1. Instrument your serving container to log predictions and features
2. Use Evidently AI to compute data drift between training and production data
3. Expose Prometheus metrics (request count, latency, prediction distribution)
4. Create a Grafana dashboard showing: drift score, latency p50/p99, error rate
5. Trigger a webhook (simulated retraining) when drift exceeds a threshold

---

## Phase 7: Advanced Topics & Capstone (Weeks 21-24)

**Goal**: Consolidate everything into a full-stack ML portfolio project.

### Topics
- Distributed training (PyTorch DDP, Ray Train)
- LLMOps: prompt management, RAG pipelines, guardrails
- MLOps on cloud: AWS SageMaker, GCP Vertex AI, Azure ML
- Cost optimization for ML workloads
- Security: model scanning, adversarial robustness, access control

### Materials
- [Full Stack Deep Learning](https://fullstackdeeplearning.com/)
- [Ray documentation](https://docs.ray.io/en/latest/)
- [Google Cloud MLOps guide](https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning)

### Capstone Assignment
Build an end-to-end ML system on free-tier cloud (or local K8s):

1. **Data**: Use a real dataset of your choice (e.g., NYC Taxi, Wikipedia traffic, sentiment from Twitter)
2. **Pipelines**: Automated data ingestion, validation, feature engineering, training (Prefect or Airflow)
3. **Experiments**: Tracked with MLflow, best model registered
4. **Serving**: BentoML or Ray Serve, deployed on K8s (or cloud equivalent)
5. **CI/CD**: GitHub Actions that tests, builds, and deploys
6. **Monitoring**: Evidently AI + Prometheus + Grafana for drift and performance
7. **Docs**: Architecture diagram, README, decision log

Submit as a public GitHub repo with all components containerized.

---

## Weekly Schedule Template (10-15 hrs)

| Day | Activity | Time |
|-----|----------|------|
| Mon | Read/watch lecture material | 1.5h |
| Tue | Hands-on coding (assignment work) | 2h |
| Wed | Hands-on coding | 2h |
| Thu | Reading + note-taking | 1.5h |
| Fri | Assignment continuation / review | 2h |
| Sat/Sun | Deep work or catch-up | 2-4h |

---

## Related Notes

- [[mlops]] - Map of content for MLOps topics
- [[second-brain]] - this vault project

## Next Actions

- [ ] Phase 1: Complete house-price prediction API
- [ ] Create a GitHub repo for the capstone project early, use it across all phases

## Open Questions

- Which cloud provider (if any) for the capstone? AWS free tier vs GCP free tier.
- Should the capstone use a CV/NLP dataset or tabular? Tabular is simpler to start.

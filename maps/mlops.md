---
title: MLOps
created: 2026-07-13
tags:
  - map
  - mlops
  - machine-learning
  - devops
---

# MLOps

Map of content for MLOps — applying DevOps practices to machine learning systems. Entry point for the [[mlops-learning-roadmap]] project.

## Core MLOps Concepts
- ML model lifecycle: data → train → evaluate → deploy → monitor → retrain
- [[experiment-tracking]] - Logging parameters, metrics, and artifacts
- [[data-versioning]] - Versioning datasets alongside code
- [[ml-pipelines]] - Automated, reproducible workflows
- [[model-serving]] - REST, gRPC, batch, streaming inference
- [[model-monitoring]] - Data drift, concept drift, performance decay
- [[feature-stores]] - Centralized feature management for training and serving

## Tool Ecosystem

| Layer | Tools |
|-------|-------|
| Experiment tracking | MLflow, Weights & Biases, Neptune |
| Data versioning | DVC, LakeFS |
| Orchestration | Prefect, Airflow, Kubeflow, Dagster |
| Serving | BentoML, Ray Serve, MLflow Serving, Seldon Core |
| Feature store | Feast, Tecton |
| Data validation | Great Expectations, Pandera, TensorFlow Data Validation |
| Monitoring | Evidently AI, WhyLabs, Prometheus + Grafana |
| CI/CD | GitHub Actions, GitLab CI, ArgoCD |
| Infrastructure | Terraform, Helm, Pulumi |
| Cloud platforms | AWS SageMaker, GCP Vertex AI, Azure ML |

## Learning Path

See [[mlops-learning-roadmap]] for the full 24-week plan.

## Key Principles
- Reproducibility first: every run should be traceable to code, data, and config
- Test data and models the same way you test code
- Automate the feedback loop: monitor → alert → retrain → deploy
- Treat ML experiments like software releases with versioning and rollback

## Related Maps
- [[projects]] - All active projects

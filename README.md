
# 🚀 MLOps Sentiment Analyzer Project: End-to-End ML System on AWS with CI/CD, Monitoring, and Kubernetes

![MLFlow](https://img.shields.io/badge/Experiment%20Tracking-MLflow-blue)
![DVC](https://img.shields.io/badge/Version%20Control-DVC-orange)
![Docker](https://img.shields.io/badge/Containerized-Docker-blue)
![Kubernetes](https://img.shields.io/badge/Deployment-EKS-informational)
![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-green)
![Monitoring](https://img.shields.io/badge/Monitoring-Prometheus%20%26%20Grafana-red)

A full-fledged MLOps project that takes a machine learning model from development to scalable production with automation, monitoring, and infrastructure on AWS.

---

## 📁 Project Structure Setup

> Based on the `cookiecutter-data-science` template for modularity.

```bash
conda create -n atlas python=3.10
conda activate atlas
pip install cookiecutter
cookiecutter -c v1 https://github.com/drivendata/cookiecutter-data-science
# Rename src.models -> src.model
````

---

## 🔬 Experiment Tracking with MLflow on Dagshub

* Connected GitHub repo to Dagshub
* Set up MLflow tracking URI from Dagshub dashboard
* Installed necessary tools:

```bash
pip install dagshub mlflow
```

* Experiments logged and tracked via MLflow UI on Dagshub.

---

## 📦 Data Versioning with DVC

```bash
dvc init
dvc remote add -d mylocal local_s3  # Temporary local remote
```

### 📊 DVC Pipeline Stages

| Stage               | Script                   |
| ------------------- | ------------------------ |
| Data Ingestion      | `data_ingestion.py`      |
| Data Preprocessing  | `data_preprocessing.py`  |
| Feature Engineering | `feature_engineering.py` |
| Model Training      | `model_building.py`      |
| Evaluation          | `model_evaluation.py`    |
| Model Registry      | `register_model.py`      |

```bash
dvc repro  # Run the pipeline
dvc status # Check changes
```

---

## ☁️ S3 as Remote Storage

* Created AWS IAM User and S3 bucket
* Configured AWS CLI:

```bash
pip install dvc[s3] awscli
aws configure
dvc remote add -d myremote s3://<bucket-name>
```

---

## 🌐 REST API with Flask

* Flask app created inside `flask_app/`
* Dependencies captured using `pipreqs`
* CI Tests organized under `tests/` and `scripts/`

---

## 🐳 Docker Containerization

```bash
docker build -t capstone-app:latest .
docker run -p 8888:5000 -e CAPSTONE_TEST=<token> capstone-app:latest
```

* Optional: Push image to DockerHub
* Environment secrets managed securely

---

## ⚙️ CI/CD with GitHub Actions

* Automated build, test, Docker image push to ECR
* Secrets and tokens managed in GitHub repo
* Workflow defined in `.github/workflows/ci.yaml`

---

## ☸️ Kubernetes Deployment on AWS EKS

```bash
eksctl create cluster \
  --name flask-app-cluster \
  --region us-east-1 \
  --nodegroup-name flask-app-nodes \
  --node-type t3.small \
  --nodes 1 --managed
```

* Kubernetes manifests: `deployment.yaml`, `service.yaml`
* External access through LoadBalancer:

```bash
kubectl get svc flask-app-service
curl http://<external-ip>:5000
```

---

## 📈 Monitoring with Prometheus & Grafana

### 🔹 Prometheus

* Ubuntu EC2 for Prometheus
* Configured to scrape Flask app metrics

```yaml
scrape_configs:
  - job_name: "flask-app"
    static_configs:
      - targets: ["<external-ip>:5000"]
```

### 🔸 Grafana

* Ubuntu EC2 for Grafana
* Connected to Prometheus as a data source
* Dashboards created for live app monitoring

---

## 🧹 AWS Resource Cleanup

* Delete deployments, services, secrets via `kubectl`
* Tear down EKS cluster:

```bash
eksctl delete cluster --name flask-app-cluster --region us-east-1
```

* Clean up ECR, S3, CloudFormation stacks

---

## 📌 Key Tools & Technologies

| Category            | Tools/Services Used  |
| ------------------- | -------------------- |
| Project Templating  | Cookiecutter         |
| Experiment Tracking | MLflow + Dagshub     |
| Data Versioning     | DVC + AWS S3         |
| Model Serving       | Flask                |
| Containerization    | Docker               |
| CI/CD               | GitHub Actions + ECR |
| Deployment          | Kubernetes (EKS)     |
| Monitoring          | Prometheus + Grafana |

---

## 🤝 Connect

> If you're a recruiter, collaborator, or curious engineer—feel free to connect or reach out for project insights or potential opportunities.




# OC Pipelines CI/CD Sample (GitHub Actions + Tekton)

A tiny Python service used to demonstrate **CI (GitHub Actions)** and **CD (OpenShift Pipelines / Tekton)**.

## Service
- Runs on **port 8000**
- Prints a startup log containing **SERVICERUNNING**

## Local run
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python app.py
```
Open: http://localhost:8000/health

## CI (GitHub Actions)
Workflow file:
- `.github/workflows/workflow.yml`

It runs:
- `flake8` lint
- `nosetests` unit tests

## CD (Tekton)
Tekton manifests:
- `.tekton/tasks.yml` (cleanup + flake8 + nose)
- `.tekton/pipeline.yml` (cleanup → git-clone → flake8 → nose → buildah → deploy)

> Your OpenShift cluster must provide the `git-clone`, `buildah`, and `openshift-client` ClusterTasks.

## Deploy manifests
- `k8s/deployment.yaml`
- `k8s/service.yaml`

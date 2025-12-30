# Behemoth App Manifests

This repository contains the Kubernetes manifests and ArgoCD configurations for the **Behemoth** application ecosystem. It follows a GitOps approach for managing both application services and infrastructure components.

## Architecture Overview

The project is structured into three main categories:

1.  **Application Services (`apps/`)**: Microservices that form the core of the Behemoth platform.
2.  **Platform Infrastructure (`platform/`)**: Essential services like databases and monitoring tools.
3.  **ArgoCD Configurations (`argocd/`)**: Application definitions for automated deployment.

### Application Services

- **Auth Service**: Node.js based authentication service.
- **Catalog Service**: Node.js based service for managing product catalogs.
- **Review Service**: Node.js based service for user reviews.
- **Frontend (FE)**: Preact-based web interface.

### Platform Components

- **Database**: PostgreSQL (managed via Bitnami Helm charts).
- **Monitoring & Logging**:
  - **Prometheus**: Metrics collection.
  - **Grafana**: Visualization dashboards.
  - **Loki**: Log aggregation.

## Deployment Strategy

This repository utilizes the **App-of-Apps** pattern with ArgoCD.

### Prerequisites

- A Kubernetes cluster.
- ArgoCD installed in the `argocd` namespace.

### Bootstrap

To deploy the entire stack, apply the root application manifest:

```bash
kubectl apply -f argocd/root-app.yaml
```

ArgoCD will automatically discover and sync all applications defined in `argocd/apps/`.

## Repository Structure

```text
.
├── apps/                   # Kustomize manifests for application services
│   ├── behemoth-nodejs-auth-service/
│   ├── behemoth-nodejs-catalog-service/
│   ├── behemoth-nodejs-review-service/
│   └── behemoth-preact-fe/
├── platform/               # Helm values and configurations for platform tools
│   ├── postgres/
│   ├── prometheus/
│   ├── grafana/
│   └── loki/
└── argocd/                 # ArgoCD Application manifests
    ├── root-app.yaml       # The "App of Apps" entry point
    └── apps/               # Individual ArgoCD app definitions
```

![architecture](./architecture.png)

## GitOps Workflow

1.  Modify manifests in `apps/` or `platform/`.
2.  Commit and push changes to the repository.
3.  ArgoCD detects the changes and synchronizes the cluster state automatically.

## License

[Specify License, e.g., MIT]

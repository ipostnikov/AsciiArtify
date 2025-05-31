# MVP — AsciiArtify

## Overview

This is the Minimum Viable Product (MVP) version of **AsciiArtify**, deployed using **ArgoCD** and **Kubernetes**. The goal is to demonstrate a fully functional GitOps pipeline, where application updates are automatically deployed to a Kubernetes cluster based on changes in a Git repo.

## Core Functionality

- Deployment of the demo application [`go-demo-app`](https://github.com/den-vasyliev/go-demo-app) using ArgoCD.
- Configured **automatic synchronization** between the Git repository and the Kubernetes cluster.
- ArgoCD continuously monitors the `main` branch of the deployment repository.
- Every change pushed to Git is **automatically deployed** to the cluster.

## Infrastructure Setup

- Kubernetes cluster (k3d).
- ArgoCD installed in the cluster.
- GitHub repository with deployment YAML manifests.
- ArgoCD Web UI for monitoring sync status and application health.

## Demonstration


- [Watch the demo video](https://drive.google.com/file/d/12u2bqgVWWuNZbmMs6GjlxGlYx670b5Gn/view?usp=sharing) — overview of the application and deployment
- [ArgoCD Auto Sync demo](https://drive.google.com/file/d/1JPdvtnNEOsU3FyQHDm_CbL3fN6_h_xxa/view?usp=sharing) — shows how ArgoCD automatically syncs Git changes to the cluster


## Conclusion

This MVP shows how GitOps with ArgoCD can simplify and automate the deployment process. It sets the stage for continuous integration and delivery, making it easier to roll out updates quickly.

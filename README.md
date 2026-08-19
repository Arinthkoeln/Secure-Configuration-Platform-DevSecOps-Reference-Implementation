# Secure Configuration Platform — DevSecOps Project

A React / Django REST configuration-management app, deployed through a
security-gated CI/CD pipeline onto a self-hosted Kubernetes cluster.
Everything below the application layer is defined as code.

> **Status:** just started. The checklist below shows what is done so far.

## Goal

Build a complete DevSecOps pipeline on my own hardware — no managed cloud
services — where security checks block a bad build instead of just reporting
on it, and the whole environment can be rebuilt from a bare Ubuntu host.

The application domain comes from my master's thesis at ETAS (Robert Bosch
GmbH). No Bosch code, data, or internal architecture is in this repository;
the app here is written from scratch.

## Planned stack

| Layer | Tool |
|---|---|
| Host provisioning | Ansible |
| Platform as code | Terraform (kubernetes, helm, docker providers) |
| Orchestration | k3s |
| CI | GitLab CI |
| SAST | SonarQube |
| Dependency scanning | OWASP Dependency-Check |
| Image scanning | Trivy |
| GitOps delivery | ArgoCD |
| Monitoring | Prometheus + Grafana |
| Application | React, Django REST, PostgreSQL |

## Pipeline design

```
push → lint → test → SAST → SCA → build → image scan → push → ArgoCD sync
```

Each security stage is blocking: SonarQube on a failed quality gate,
Dependency-Check on CVSS ≥ 7, Trivy on HIGH/CRITICAL findings.

## Progress

- [ ] Ansible host provisioning
- [ ] Terraform platform definition
- [ ] Django REST backend with role-based access control
- [ ] React frontend
- [ ] Hardened multi-stage Dockerfile (non-root, minimal base)
- [ ] GitLab CI pipeline with blocking security gates
- [ ] ArgoCD GitOps sync
- [ ] Prometheus + Grafana dashboards

## Setup

Requirements: Ubuntu 22.04, 8 GB RAM, 40 GB disk.

```bash
git clone https://github.com/Arinthkoeln/<REPO>.git
cd <REPO>
```

Setup instructions will be added as each component lands.

## Notes

Running log of what broke and how I fixed it — added as I go.

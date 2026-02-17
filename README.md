# Building Self-Service Provisioning on OpenShift  - NB Internal Developer Platform
A Sample self service provisioning for NB developers on OpenShift 

ARCHITECTURE OVERVIEW

┌─────────────────────────────────────────────────────────────────┐
│              Developer Self-Service Flow                         │
│                                                                  │
│   Developer                                                      │
│      │                                                           │
│      ▼                                                           │
│  ┌──────────────────┐                                           │
│  │ Red Hat Dev Hub  │  ← Self-service portal (Backstage)        │
│  │ (RHDH/Backstage) │                                           │
│  └────────┬─────────┘                                           │
│           │ Submits request via Software Template               │
│           ▼                                                      │
│  ┌──────────────────┐                                           │
│  │   Git Repo       │  ← Single source of truth                 │
│  │  (GitLab/GitHub) │                                           │
│  └────────┬─────────┘                                           │
│           │ ArgoCD watches repo                                  │
│           ▼                                                      │
│  ┌──────────────────┐                                           │
│  │ OpenShift GitOps │  ← Reconciles desired state               │
│  │    (ArgoCD)      │                                           │
│  └────────┬─────────┘                                           │
│           │ Applies to cluster                                   │
│           ▼                                                      │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │                  OpenShift Cluster                        │  │
│  │                                                           │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │  │
│  │  │  Namespace  │  │  Namespace  │  │  Namespace  │     │  │
│  │  │  (Team A)   │  │  (Team B)   │  │  (Team C)   │     │  │
│  │  │             │  │             │  │             │     │  │
│  │  │ RBAC        │  │ RBAC        │  │ RBAC        │     │  │
│  │  │ Quotas      │  │ Quotas      │  │ Quotas      │     │  │
│  │  │ NetworkPol  │  │ NetworkPol  │  │ NetworkPol  │     │  │
│  │  │ LimitRange  │  │ LimitRange  │  │ LimitRange  │     │  │
│  │  └─────────────┘  └─────────────┘  └─────────────┘     │  │
│  │                                                           │  │
│  │  ┌─────────────────────────────────────────────────┐    │  │
│  │  │  Governance Layer (ACM Policies + Kyverno)      │    │  │
│  │  └─────────────────────────────────────────────────┘    │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘

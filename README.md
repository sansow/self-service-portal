# Building Self-Service Provisioning on OpenShift  - NB Internal Developer Platform
This repository drives the **NB's Internal Developer Platform** on OpenShift.
It implements a self-service provisioning model that gives application teams cloud-like
agility while enforcing enterprise security, governance, and compliance at scale.


**Platform Owner:** Team Platform Engineering
**Platform:** Red Hat OpenShift on-prem

nb-platform-gitops/
├── base/
│   ├── namespace-template/         # Base namespace manifests (applied to all teams)
│   │   ├── namespace.yaml          # Namespace definition
│   │   ├── rbac.yaml               # Role bindings (AD group integration)
│   │   ├── network-policies.yaml   # Zero-trust network policies
│   │   └── kustomization.yaml
│   ├── quotas/
│   │   └── quotas.yaml             # Small / Medium / Large resource tiers
│   ├── policies/
│   │   └── kyverno-policies.yaml   # Governance & compliance policies
│   └── addons/
│       ├── kafka-access/           # Enable Kafka/EDA network access
│       ├── service-mesh/           # Enable Istio sidecar injection
│       └── gpu-resources/          # Enable GPU resource allocation
├── clusters/
│   ├── production/
│   │   ├── argocd-applicationset.yaml  # Auto-provisions namespaces from Git
│   │   └── namespaces/
│   │       ├── trading-prod/           # Example: Trading team production
│   │       ├── risk-prod/              # Example: Risk team production
│   │       └── compliance-prod/        # Example: Compliance team production
│   └── staging/
│       └── namespaces/
├── rhdh/
│   └── namespace-request-template.yaml # Red Hat Developer Hub self-service form
├── monitoring/
│   └── chargeback-rules.yaml           # Cost tracking per namespace/team
└── scripts/
    └── new-namespace.sh                # CLI provisioning script
```

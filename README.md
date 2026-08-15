# backend

Node.js API for the Expense app (transaction service, MySQL-backed). Part of the [Expense project](https://github.com/akhildanda/expense-infra-dev).

## Role in the Expense project

This repo's Jenkins pipeline is the entry point for shipping a new backend version. It currently builds and deploys via the **container path**:

```
git push  ──>  Jenkins (this repo)
                 ├─ read version from package.json
                 ├─ docker build → push to ECR
                 └─ helm install (helm/ chart) → EKS cluster "expense-dev"
                     (cluster provisioned by terraform-aws-eks / k8-eksctl)
```

A VM-path route also exists in history (build zip → upload to Nexus → trigger [backend-deploy](https://github.com/akhildanda/backend-deploy)), matching how [frontend](https://github.com/akhildanda/frontend) ships today — see the note on path consistency in the [hub README](https://github.com/akhildanda/expense-infra-dev#known-limitations--roadmap).

## Contents

- `index.js`, `TransactionService.js`, `DbConfig.js` — app source
- `schema/` — MySQL schema imported by the `expense-ansible-roles-tf` backend role
- `helm/` — Helm chart used to deploy to EKS
- `Dockerfile` — container build definition
- `Jenkinsfile` — CI/CD pipeline

## Related repos

See the full architecture and repo map in [expense-infra-dev](https://github.com/akhildanda/expense-infra-dev#repositories-in-this-project).

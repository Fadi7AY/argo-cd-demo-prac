# Argo CD · environment demo

Kubernetes manifests arranged by environment, plus an Argo CD Application definition.


```mermaid
flowchart LR
    Git["Git source · development path"] --> Argo["Argo CD Application"]
    Argo --> Cluster["Kubernetes · argocd-demo namespace"]
    Cluster -. Drift reconciliation .-> Argo
```


## Before applying

[argo-application.yaml](argo-application.yaml) currently points to **anveshmuppeda/argo-cd-demo**,
not this fork. Set `spec.source.repoURL`, `targetRevision` and `path` to the repository and environment you intend to deploy.

The manifest enables automated sync, pruning, self-healing and namespace creation.

## Environment folders

| Folder | Role |
| --- | --- |
| [development](development) | Deployment and Service manifests; the Application selects this path. |
| [beta](beta) | Beta environment manifests. |
| [prod](prod) | Production environment manifests. |

## Apply the Application

With Argo CD already installed and the source reviewed:

```bash
kubectl apply -f argo-application.yaml
```

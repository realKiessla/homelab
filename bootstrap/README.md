# Cluster Bootstrapping
We are using the ArgoCD pattern `App of Apps` to deploy multiple of our applications for an easy bootstrapping process.

## Structure
### [argocd](argocd)
The Helm Chart responsible for installing ArgoCD to a newly created cluster.

### [applications](applications)
The `App of Apps` (or `root`) Helm Chart. In this Helm Chart there are all applications listed that should be installed by ArgoCD
when initially bootstrapping a newly created cluster. 

## Getting Started
1. Install the `ArgoCD` Helm Chart. Specific instructions can be found in the [argocd directory](argocd).
2. Create and sync the `App of Apps` Helm Chart inside ArgoCD, either via UI or CLI.

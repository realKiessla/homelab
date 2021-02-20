# Longhorn Installation
## Prerequisite
The only thing that had to be installed on our Raspberry PI 4's with Ubuntu 20.04 LTS was the package `nfs-common`.

## Installation
We are using a slightly extended version of longhorn, and because of that don't install the Helm chart directly from the repository.

Use the following commands to install Longhorn:

    kubectl create namespace longhorn-system
    helm install longhorn . --namespace longhorn-system

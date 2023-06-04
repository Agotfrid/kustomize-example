# kustomize-example

This repository contains Kubernetes resource configurations managed using Kustomize. They are meant to be deployed to a Kubernetes cluster either manually or automatically via ArgoCD.

## Prerequisites

Ensure you have the following before starting:

1. Access to a Kubernetes cluster.
2. ArgoCD installed in the cluster (only for automatic deployment).
3. kubectl and kustomize installed on your local machine.

## Manual Deployment

Ensure that you've selected the correct Kubernetes context if you have access to multiple clusters.
To manually deploy these resources to your cluster, navigate to the root directory of this repository and run the following command:

```
kubectl apply -k overlays/develop
```

## Automatic Deployment with ArgoCD

To manage these resources automatically using ArgoCD, you need to have ArgoCD installed and running in your cluster. 

Apply `application.yaml` and `project.yaml` to the `argocd` namespace to make sure argocd will monitor and sync changes in kustomize repo:

```
kubectl apply -f argocd/project.yaml -n argocd
kubectl apply -f argocd/application.yaml -n argocd
```

This creates an ArgoCD project and application that will monitor changes in the `main` branch of this repository and sync them to the cluster.

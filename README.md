# Workshop Jenkins

This repository is intended to contain support files for Kubemotion's workshops about deploying Jenkins on Kubernetes.

![Jenkins & Kubenretes logos](https://i.imgur.com/VvsoWJw.png)

## Dependencies
  - A running cluster and kubectl configured.
  - helm.

## Installation

Initialize `helm` if not already initialized use the following commands depending if RBAC is enabled on your cluster:
```bash
# Without RBAC
helm init
```

```bash
# With RBAC
# Create a tiller service account with the rbac.yml file on this repository root."
kubectl create -f rbac.yml

helm init --service-account tiller
```

Install jenkins using helm

```bash
# Without RBAC
helm install --name kubejenkins stable/jenkins

# With RBAC
helm install --name kubejenkins stable/jenkins --set rbac.install=true
```

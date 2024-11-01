

## Create Kubernetes Cluster ##
- kind create cluster --name rbac --image kindest/node:v1.31.0

## Install Kyverno ##
- kubectl apply --server-side=true -f https://github.com/kyverno/kyverno/releases/download/v1.13.0/install.yaml

## Create Kyverno Policies ##
- kubectl apply -f policies/pods/require-labels.yaml
- kubectl apply -f policies/pods/require-pod-probes.yaml
- kubectl apply -f policies/pods/require-pod-requests-limits.yaml

## Create Service Account and Roles ##
- kubectl apply -f junior-developer/readonly-role.yaml
- kubectl apply -f junior-developer/readonly-role-binding.yaml
- kubectl apply -f junior-developer/service-account.yaml
- kubectl apply -f junior-developer/service-account-secret.yaml

## SetUp Kubeconfig ##
- kubectl describe secret/junior-developer-secret
- get token from previous command and set in token key of junior-developer/junior-developer.kubeconfig

## Test Kubectl with new kubectconfig ##
- kubectl --kubeconfig=./junior-developer/junior-developer.kubeconfig get pods
# Kubernetes Cluster Components
Follow this guide to install various cluster components

## NGINX Ingress Controller
```
helm upgrade --install nginx-ingress -n=nginx-ingress --create-namespace oci://registry-1.docker.io/bitnamicharts/nginx-ingress-controller --set ingressClassResource.default=true
```

## Cert Manager
```
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.12.0/cert-manager.yaml
```

## Rancher
```
helm repo add rancher-latest https://releases.rancher.com/server-charts/latest

helm install rancher rancher-latest/rancher \
  --namespace cattle-system \
  --create-namespace \
  --set hostname=rancher.k8s.decrinis.com \
  --set bootstrapPassword=admin \
  --set ingress.tls.source=letsEncrypt \
  --set global.cattle.psp.enabled=false

```

## Nvidia Operator
```
helm repo add nvidia https://helm.ngc.nvidia.com/nvidia

helm install --wait --generate-name \
     -n gpu-operator --create-namespace \
     nvidia/gpu-operator
```

## Kube Invaders
```
helm repo add kubeinvaders https://lucky-sideburn.github.io/helm-charts/

helm upgrade --install kubeinvaders -n kubeinvaders --create-namespace kubeinvaders/kubeinvaders -f kubeinvaders-answer.yml
```
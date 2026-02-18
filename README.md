# d3-deploy

## Kubernetes

Ingress: kubectl apply
-f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
Metrics: kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml и
добавить - --kubelet-insecure-tls в metric-deployment

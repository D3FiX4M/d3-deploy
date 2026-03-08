# Metrics:
## helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
## kubectl create namespace monitoring

## Node Exporter (CPU, RAM, диск, сеть) 
### helm install node-exporter prometheus-community/prometheus-node-exporter --namespace monitoring

## kube-state-metrics (количество подов, деплойментов, статус нод и т.д)
### helm install kube-state-metrics prometheus-community/kube-state-metrics --namespace monitoring

# Storages:
## kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml (для PVC)


## MinIO (для mimir, loki, tempo)
## helm install minio minio/minio --namespace monitoring -f minio-values.yaml

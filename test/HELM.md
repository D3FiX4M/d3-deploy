# Taint
    1) kubectl taint nodes k3s-master node-role.kubernetes.io/master=:NoSchedule

# Namespace
    1) kubectl create ns monitoring
    2) kubectl create ns logging
    3) kubectl create ns tracing
    2) kubectl create ns database
    3)

# Ingress
    1) helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
    2) helm upgrade --install ingress-nginx ingress-nginx/ingress-nginx \
        --namespace ingress-nginx \
        --create-namespace \
        --set controller.ingressClassResource.name=nginx \
        --set controller.ingressClassResource.default=true \
        --set controller.metrics.enabled=true \
        --set controller.metrics.serviceMonitor.enabled=true \
        --set controller.service.externalIPs[0]=192.168.1.100

# Cert-manager
    1) helm repo add jetstack https://charts.jetstack.io
    2) kubectl apply -f https://github.com/cert-manager/cert-manager/releases/latest/download/cert-manager.crds.yaml
    3) helm upgrade --install cert-manager jetstack/cert-manager \
        --namespace cert-manager \
        --create-namespace \
        --set prometheus.servicemonitor.enabled=true 
    4)selfsigned version: kubectl apply -f root-certs.yaml 
    
    P.S. label: cert-manager.io/cluster-issuer: d3-ca-issuer
    P.S.1. Вытащить cc для импорта: kubectl get secret d3-ca -n cert-manager -o jsonpath="{.data.tls\.crt}" | base64 -d > d3-ca.crt

# Grafana
    1) helm upgrade --install grafana grafana-community/grafana -n monitoring -f values.yaml
    
# Metrics
    1) kubectl create ns monitoring
    2) kubectl apply -f monitoring-cert.yaml
    3) helm upgrade --install kube-prometheus-stack oci://ghcr.io/prometheus-community/charts/kube-prometheus-stack \
        -n monitoring \
        -f values.yaml

# MinIO
    1) kubectl create ns datasource
    2) kubectl apply -f minio-cert.yaml
    3) helm upgrade --install minio minio/minio \
        --namespace datasource \
        -f values.yaml

# Logging
    1) helm upgrade --install loki grafana-community/loki -n monitoring -f values.yaml
    2) helm upgrade --install fluent-bit fluent/fluent-bit -n monitoring -f values.yaml



# Strimzi
    1) helm upgrade --install strimzi-kafka-operator \
        oci://quay.io/strimzi-helm/strimzi-kafka-operator \
        --namespace messaging

        helm uninstall strimzi-kafka-operator \
        -n messaging
    
    2) kubectl apply -n messaging -f cluster.yaml && \
       kubectl apply -n messaging -f metrics/metrics-configmap.yaml && \
       kubectl apply -n messaging -f metrics/podMonitor.yaml && \
       kubectl apply -n messaging -f topic/test-topic.yaml && \
       kubectl apply -n messaging -f user/d3-user.yaml && \
       kubectl apply -n messaging -f metrics/kube-state-metrics/configmap.yaml && \
       kubectl apply -n messaging -f metrics/kube-state-metrics/ksm.yaml

    3) kubectl delete -n messaging -f cluster.yaml
       kubectl delete -n messaging -f metrics/metrics-configmap.yaml
       kubectl delete -n messaging -f metrics/podMonitor.yaml
       kubectl delete -n messaging -f topic/test-topic.yaml
       kubectl delete -n messaging -f user/d3-user.yaml
       kubectl delete -n messaging -f metrics/kube-state-metrics/configmap.yaml
       kubectl delete -n messaging -f metrics/kube-state-metrics/ksm.yaml

# Tempo
    1) helm upgrade --install tempo grafana-community/tempo -n tracing -f values.yaml


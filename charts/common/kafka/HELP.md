helm repo add rhcharts https://ricardo-aires.github.io/helm-charts/
helm repo update
helm install kafka rhcharts/kafka -n kafka -f kafka-values.yaml --create-namespace
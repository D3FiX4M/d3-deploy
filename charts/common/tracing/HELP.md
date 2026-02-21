helm repo add jaegertracing https://jaegertracing.github.io/helm-charts
helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts
helm repo update


helm install jaeger jaegertracing/jaeger \
--namespace d3-tracing \
--set allInOne.enabled=true \
--set collector.service.otlp.enabled=true \
--set query.ingress.enabled=false

helm install otel-collector open-telemetry/opentelemetry-collector \
--namespace d3-tracing \
-f otel-collector-values.yaml
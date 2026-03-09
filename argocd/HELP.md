# Установка Argo CD:
    helm repo add argo https://argoproj.github.io/argo-helm
    helm install argocd argo/argo-cd --namespace argocd --create-namespace -f argocd/config.yaml

### Получения пароля:
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
### Доступ через ingress argocd.d3.local/

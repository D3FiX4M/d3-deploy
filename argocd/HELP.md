# Установка Argo CD:
### 1) helm repo add argo https://argoproj.github.io/argo-helm
### 2) kubectl create ns argocd
### 3) helm install argocd argo/argo-cd -n argocd -f argocd/config.yaml
## ---
## Получения пароля:
### kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
### Доступ через port-forward или  ingress argocd.d3.local/

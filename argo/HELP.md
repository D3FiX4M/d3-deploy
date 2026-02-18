ArgoCD:
1)helm repo add argo https://argoproj.github.io/argo-helm
2)helm repo update
3)kubectl create namespace argocd
4)helm install argo-cd argo/argo-cd -n argocd -f argo-values.yml
5)kubectl port-forward service/argo-cd-argocd-server -n argocd 8082:443
6)kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
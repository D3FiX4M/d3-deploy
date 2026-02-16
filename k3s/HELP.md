# Установка k3s кластера

## CP1:
### VM конфигурация:
    Система: 4 RAM, 2 CPU, 25 GB
    Сеть: enp0s3 - NAT (Нужен для подключения к VPN с хоста, чтобы скачивать образы), enp0s8 - Bridge (Static ip 192.168.1.100)
### Установка:
    Отключения firewall: ufw disable
    Установка: curl -L https://get.k3s.io | sh -s - server --cluster-init --flannel-iface "enp0s8" --disable=traefik
    P.S.1. traefik отключается, чтобы поставить nginx
    P.S.2. server --cluster-init нужно, чтобы задать master node, для возможности репликации CP{N} в дальнейшем
    P.S.3. kubeconfig лежит в /etc/rancher/k3s/k3s.yaml

## WR:
### VM конфигурация:
    Система: 8 RAM, 4 CPU, 50 GB
    Сеть: enp0s3 - NAT (Нужен для подключения к VPN с хоста, чтобы скачивать образы), enp0s8 - Bridge (Static ip 192.168.1.200)    
### Установка
    Отключение firewall: ufw disable
    Установка: curl -L https://get.k3s.io | K3S_URL="https://192.168.1.100:6443" \
      K3S_TOKEN='' \
      INSTALL_K3S_EXEC="--flannel-iface enp0s8" \
      sh -
    P.S.1. K3S_TOKEN достается из mater node через cat /var/lib/rancher/k3s/server/node-token


## HOST:
### Переключение context
    kubectl config use-context k3s
### Установка ingress-nginx
    helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
    helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx --create-namespace
### Taint
    kubectl taint nodes cp1 node-role.kubernetes.io/master=:NoSchedule
### Установка Argo CD
[Продолжение](../argocd/HELP.md)
    
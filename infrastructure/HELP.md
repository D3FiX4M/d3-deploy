# Vagrant

# Ansible
    1) Проверить ping: ansible -i ansible/inventory.yaml all -m ping
    2) Сбросить ssh ключи: ssh-keygen -f /home/d3fix4m/.ssh/known_hosts -R 192.168.1.100
    3) Запуск кластера в full режиме: ansible-playbook -i ansible/inventory.yaml ansible/playbooks/full_cluster.yaml

# Kubeconfig
    1) Положить в директорию .kube, где лежит основной config
    2) Выполнить команды:
        a. $env:KUBECONFIG="config;k3s-config.yaml"
        b. kubectl config view --merge --flatten > temp-config
        c. Move-Item -Path temp-config -Destination config -Force
        d. kubectl config use-context k3s
## Создаем секрет с кредами докер хаба

kubectl create secret docker-registry docker-hub-secret \
--docker-server=https://index.docker.io/v1/ \
--docker-username=USERNAME \
--docker-password=PASSWORD \
-n d3

## Устанавливаем serviceAccount

kubectl apply -f service-account.yml

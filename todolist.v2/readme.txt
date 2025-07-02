Предварительные требования
   - Установленный Kubernetes кластер
   - Установленный Helm (версии 3.x)
   - Доступ к кластеру через kubectl

1. Клонирование репозитория
   git clone https://github.com/sudolicious/k8s/todolist.v2

2. Добавление репозитория Bitnami
   helm repo add bitnami https://charts.bitnami.com/bitnami
   helm repo update

3. Установите local path provisioner (для bare-metal)
   kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.24/deploy/local-path-storage.yaml
   
4. Настройка хранилища (для bare-metal). На каждой ноде создайте директорию:   
   sudo mkdir -p /mnt/data/postgres
   sudo chown -R 1001:1001 /mnt/data/postgres

5. Создание секрета с паролем
   kubectl create secret generic postgres-secret   --from-literal=POSTGRES_PASSWORD=your_password

6. Установка PostgreSQL
   helm install postgres bitnami/postgresql -f postgres/values.yaml

7. Запуск бэкэнда
   helm install backend ./backend
   
8. Запуск фронтэнда
   helm install frontend ./frontend

Проверка подов: 
   kubectl get po -A

Доступ к приложению: http://<node-ip>:30007

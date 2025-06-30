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
   sudo chmod 777 /mnt/data/postgres

5. Создание секрета с паролем
   kubectl create secret generic postgres-secret   --from-literal=POSTGRES_PASSWORD=1234

6. Установка PostgreSQL с конфигурацией
   cd postgres/
   helm install postgres bitnami/postgresql -f values.yaml

8. Проверка подключения

   # Дождитесь перехода pod в статус Running:
   kubectl get pods -A

9. Запуск бэкэнда
   cd ..
   kubectl apply -f ./backend

   Бэкэнд: http://localhost:30007/api/tasks
   
10. Запуск фронтэнда
   kubectl apply -f ./frontend
   
   Фронтэнд: http://localhost:30007

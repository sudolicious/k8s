Предварительные требования
   - Установленный Kubernetes кластер
   - Доступ к кластеру через kubectl

1. Клонирование репозитория
   
   git clone https://github.com/sudolicious/k8s/todolist.v1

2. Настройка хранилища (для bare-metal). На каждой ноде создайте директорию:
   
   sudo mkdir -p /mnt/data/postgres
   sudo chmod 777 /mnt/data/postgres

3. Создание секрета с паролем
   
   kubectl create secret generic postgres-secret   --from-literal=POSTGRES_PASSWORD=1234

4. Установка PostgreSQL

   kubectl apply -f ./postgres

   # Дождитесь перехода pod в статус Running:
   kubectl get pods -A

5. Запуск бэкэнда

   kubectl apply -f ./backend
   
   # Дождитесь перехода pod в статус Running:
   kubectl get pods -A

   Бэкэнд: http://<node-ip>:30007/api/tasks
   
6. Запуск фронтэнда

   kubectl apply -f ./frontend

   # Дождитесь перехода pod в статус Running:
   kubectl get pods -A

   Фронтэнд: http://<node-ip>:30007

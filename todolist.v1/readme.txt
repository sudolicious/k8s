Предварительные требования
   - Установленный Kubernetes кластер
   - Доступ к кластеру через kubectl

1. Клонирование репозитория   
   git clone https://github.com/sudolicious/k8s/todolist.v1

2. Настройка хранилища (для bare-metal). На каждой ноде создайте директорию:   
   sudo mkdir -p /mnt/data/postgres
   sudo chown -R 1001:1001 /mnt/data/postgres

3. Создание секрета с паролем   
   kubectl create secret generic postgres-secret   --from literal=POSTGRES_PASSWORD=your_password

4. Установка PostgreSQL
   kubectl apply -f ./postgres

5. Запуск бэкэнда
   kubectl apply -f ./backend
   Бэкэнд: http://<node-ip>:30007/api/tasks
   
6. Запуск фронтэнда
   kubectl apply -f ./frontend
   Фронтэнд: http://<node-ip>:30007

7. Проверка подов: 
   kubectl get po -A

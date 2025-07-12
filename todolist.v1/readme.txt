Kubernetes Deployment for ToDolist Application

Requirements:
- Installed Kubernetes cluster
- Access to the cluster via kubectl

1. Clone the repository
   git clone https://github.com/sudolicious/k8s
   cd todolist.v1

2. Storage setup (for bare-metal). On each node create directory:
   sudo mkdir -p /mnt/data/postgres
   sudo chown -R 1001:1001 /mnt/data/postgres

3. Create password secret
   kubectl create secret generic postgres-secret --from-literal=POSTGRES_PASSWORD=your_password

4. Install PostgreSQL
   kubectl apply -f ./postgres

5. Start backend
   kubectl apply -f ./backend
   
   Backend: http://<node-ip>:30007/api/tasks

6. Start frontend
   kubectl apply -f ./frontend
   
   Frontend: http://<node-ip>:30007

7. Check pods:
   kubectl get po -A
   

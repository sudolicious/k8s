Kubernetes Deployment for ToDolist Application 

Application is served via http://altenar-intership-2025.com

Requirements:
- Installed Kubernetes cluster
- Installed Helm (version 3.x)
- Access to the cluster via kubectl

1. Clone the repository
   git clone https://github.com/sudolicious/k8s
   cd todolist.v2

2. Add Bitnami repository
   helm repo add bitnami https://charts.bitnami.com/bitnami
   helm repo update

3. Install local path provisioner (for bare-metal)
   kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.24/deploy/local-path-storage.yaml

4. Storage setup (for bare-metal). Create directory on each node:
   sudo mkdir -p /mnt/data/postgres
   sudo chown -R 1001:1001 /mnt/data/postgres

5. Create password secret
   kubectl create secret generic postgres-secret --from-literal=POSTGRES_PASSWORD=yoursecretpassword

6. Install PostgreSQL
   helm install postgres bitnami/postgresql -f postgres/values.yaml

7. Start backend
   helm install backend ./backend
   
   Backend: http://altenar-internship-2025.com/api/tasks

8. Start frontend
   helm install frontend ./frontend

Application access: http://altenar-internship-2025.com

9. Check pods:
   kubectl get po -A


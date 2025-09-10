Kubernetes Deployment for ToDolist Application with Helm

Application is served via http://altenar-intership-2025.com (used Nginx Controller and MetalLB)

Requirements:
- Installed Kubernetes cluster
- Installed Helm (version 3.8.x)
- Access to the cluster via kubectl

1. Clone the repository
   git clone https://github.com/sudolicious/k8s
   cd k8s/todolist.v2

2. Add Bitnami repository
   helm repo add bitnami https://charts.bitnami.com/bitnami
   ( helm repo add bitnami https://raw.githubusercontent.com/bitnami/charts/archive-full-index/bitnami )
   helm repo update

3. Install local path provisioner (for bare-metal)
   kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.24/deploy/local-path-storage.yaml

4. Add name to /etc/hosts
   echo '<ip-vm> altenar-internship-2025.com' | sudo tee -a /etc/hosts

5. Install Nginx Controller
   Установка NGINX Ingress Controller
   helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
   helm repo update
   helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace
   
   Check the servise (TYPE=LoadBalancer): kubectl get svc -n ingress-nginx
   
6. Install MetalLB via Helm
   helm repo add metallb https://metallb.github.io/metallb
   helm repo update
   helm install metallb metallb/metallb --namespace metallb-system --create-namespace

7. Apply config pf Metallb
   kubectl apply -f metallb-config.yml
   
8. Install Prometheus-stack and apply manifests

9. Install Vault 
   kubectl apply -f vault.yml
   kubectl create namespace vault
   
   Check:
   kubectl get pods -n vault
   kubectl get svc -n vault
   kubectl exec -n vault -it vault-server-0 -- vault status

9. Create password secret
   kubectl create secret generic postgres-secret --from-literal=POSTGRES_PASSWORD=yoursecretpassword

10. Install PostgreSQL
   helm install postgres bitnami/postgresql -f postgres/values.yaml

8. Start backend
   helm install backend ./backend
   
   Backend: http://altenar-internship-2025.com/api/tasks
   Endpoints: kubectl get endpoints backend
   
8. Start frontend
   helm install frontend ./frontend

Application access: http://altenar-internship-2025.com

9. Check pods:
   kubectl get po -A

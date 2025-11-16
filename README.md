helm create fullstack-app

This will generate a folder named fullstack-app/ with the following structure:

fullstack-app/
├── charts/
├── templates/
├── Chart.yaml
├── values.yaml

You can then modify values.yaml and templates (deployment.yaml, service.yaml, ingress.yaml, etc.) as per your fullstack app (frontend, backend, MySQL, etc.).

⚙️ Step 2: Add and Update Helm Repositories

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm repo list
🌐 Step 3: Install NGINX Ingress Controller

🟢 First time (creates namespace)

helm install ingress-nginx ingress-nginx/ingress-nginx --create-namespace --namespace ingress-nginx

🔁 Next time (upgrade without creating namespace)

helm upgrade ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx

🔍 Check Ingress Controller Pods

kubectl get pods -n ingress-nginx

🪵 View Ingress Logs

kubectl logs -f <ingress-pod-name> -n ingress-nginx

🏗 Step 4: Install or Upgrade Your Fullstack App

🟢 First time (creates namespace)

helm install fullstack-app ./fullstack-app --create-namespace --namespace fullstack-app

🔁 Next time (upgrade without recreating namespace)

helm upgrade fullstack-app ./fullstack-app --namespace fullstack-app

🔍 Check Application Pods

kubectl get pods -n fullstack-app

🪵 View Application Logs

kubectl logs -f <backend-pod-name> -n fullstack-app
kubectl logs -f <frontend-pod-name> -n fullstack-app
kubectl logs -f <mysql-pod-name> -n fullstack-app

📋 Step 5: List Helm Releases

helm list -n fullstack-app

🧩 Step 6: Check Release Status

helm status fullstack-app -n fullstack-app

🪵 Optional: Tail logs while checking status

kubectl logs -f <backend-pod-name> -n fullstack-app

🧾 Step 7: View Manifest

helm get manifest fullstack-app -n fullstack-app

🕓 Step 8: Check Release History

helm history fullstack-app -n fullstack-app

📈 Step 9: Horizontal Pod Autoscaler (HPA)

🧩 Check All HPAs

kubectl get hpa -n fullstack-app

📋 Describe a Specific HPA

kubectl describe hpa backend -n fullstack-app
kubectl describe hpa frontend -n fullstack-app

📈 Watch Scaling in Real Time

kubectl get hpa -n fullstack-app -w

🔍 Check Current Pods and Resource Usage

kubectl get pods -n fullstack-app

⚙️ Manually Scale (Optional)

kubectl scale deployment backend-deployment --replicas=5 -n fullstack-app
kubectl scale deployment frontend-deployment --replicas=5 -n fullstack-app

🪵 Monitor Logs During Scaling

kubectl logs -f <backend-pod-name> -n fullstack-app

📊 Step 10: Monitor Pods and Scaling Activity

kubectl get pods -n fullstack-app -w

❌ Step 11: Uninstall the Fullstack App

helm uninstall fullstack-app -n fullstack-app

🧹 Step 12: Uninstall NGINX Ingress Controller

helm uninstall ingress-nginx -n ingress-nginx

🧼 Step 13: Delete Namespaces (Cleanup)

kubectl delete namespace fullstack-app
kubectl delete namespace ingress-nginx

# Hamza Advanced App

Ce projet est une application Node.js dockerisée avec déploiement Kubernetes avancé :

- ✅ Dockerfile (Node.js 18)
- 📦 App.js + .env
- 🔐 Secrets, ConfigMap, Namespace
- 🌐 Ingress NGINX avec custom domain
- 🧱 MongoDB déployée avec PVC (persistent volume)
- 📁 Arborescence claire : `app/`, `dbmongo/`, `k8s/`

## Objectif

Ce projet simule un déploiement cloud complet pour mon portfolio DevOps.

## Déploiement local

## bash
docker build -t hamza-app .
docker run -p 3000:80 hamza-app

### Déploiement Kubernetes
kubectl apply -f k8s/
kubectl apply -f dbmongo/

## 🛠️ Troubleshooting Commands (Kubernetes + Docker)
     🔧 Task Description	                                 🧪 Command
🔍 See all resources in all namespaces	         kubectl get all --all-namespaces
📦 See all pods in your namespace	               kubectl get pods -n hamza-app
🔎 Describe a specific pod	                     kubectl describe pod <pod-name> -n hamza-app
📄 View logs of a container inside a pod	       kubectl logs <pod-name> -n hamza-app
🚨 Check if service is exposing correct ports	   kubectl get svc --all-namespaces
🧪 Forward service port to localhost	           kubectl port-forward svc/hamza-service 80:8080 -n hamza-app
🧹 Delete a specific pod manually	               kubectl delete pod <pod-name> -n hamza-app
❌ Scale down deployment (before shutting down)	 kubectl scale deployment hamza-app --replicas=0 -n hamza-app
🔁 Scale up deployment (after restart)	         kubectl scale deployment hamza-app --replicas=2 -n hamza-app
📜 Check all deployments	                       kubectl get deployments -n hamza-app
📥 Reapply deployment YAML	                     kubectl apply -f deployment.yaml
🌐 Reapply service YAML	                         kubectl apply -f service.yaml
🌍 Reapply ingress YAML	                         kubectl apply -f ingress.yaml
❌ Delete ingress if needed	                     kubectl delete ingress hamza-ingress -n hamza-app
🛑 Stop all running Docker containers	           docker stop <container-id>
🧼 Remove all stopped Docker containers	         docker container prune
🔎 See all running Docker containers	           docker ps
📦 See all Docker containers (incl. stopped)	   docker ps -a
🗑️ Remove all unused Docker images	             docker image prune -a
📤 Push local image to Docker Hub	               docker push <your-dockerhub-username>/hamza-app
🔍 View logs of a Docker container	             docker logs <container-id>


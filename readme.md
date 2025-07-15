# 🚀 Hamza Advanced App

Ce projet est une application Node.js dockerisée et déployée dans un environnement Kubernetes avec une structure claire et des bonnes pratiques DevOps.

---

## ✅ Fonctionnalités principales

- 🐳 Dockerfile (Node.js 18)
- 📦 App.js avec fichier .env
- 🔐 Déploiement Kubernetes avec Secrets, ConfigMap, Namespace
- 🧱 MongoDB avec Persistent Volume
- 🌐 Ingress NGINX avec domaine personnalisé (hamza.local)
- 📁 Arborescence claire : app/, k8s/, dbmongo/

---

## 🎯 Objectif

Ce projet simule un déploiement cloud complet en local, idéal pour les environnements DevOps réels ou à des fins de formation.

---

## 📁 Structure du projet
```bash
hamza-advanced-app/
├── app/ # Code source Node.js
│ ├── app.js
│ ├── package.json
│ └── Dockerfile
├── dbmongo/ # Manifeste MongoDB
│ ├── mongo-deployment.yaml
│ └── mongo-service.yaml
├── k8s/ # Déploiement Kubernetes App
│ ├── configmap.yaml
│ ├── deployment.yaml
│ ├── ingress.yaml
│ ├── namespace.yaml
│ ├── secret.yaml
│ └── service.yaml
└── README.md
```
---
### Windows with Docker Desktop

## 🧪 Déploiement local avec Kubernetes ( Docker Desktop)

> ⚠ Assurez-vous que Kubernetes est activé et que l’Ingress Controller (comme NGINX) est installé.
## Installer l’Ingress Controller NGINX (si ce n’est pas déjà fait)
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.0/deploy/static/provider/cloud/deploy.yaml
## Vérifier que tout fonctionne
```bash
kubectl get all -n ingress-nginx
kubectl get ingress
```
 In the first we need to clone the repo in the local with this command"
```bash
git clone https://github.com/hamzahssaini/Kubernetes-Project.git
cd Kuberbetes-Project
```
### 🧱 1. Créer le namespace
```bash
kubectl apply -f k8s/namespace.yaml
```
## 🗃 2. Déployer MongoDB
```bash
kubectl apply -f dbmongo/
```
## 🚀 3. Déployer l’application Node.js
```bash
kubectl apply -f k8s/
```
## 🌐 Accès à l’application
✅ Option A – Accès via Ingress (domaine personnalisé)

Ajoutez la ligne suivante ( 127.0.0.1 hamza.local ) sur 
 C:\Windows\System32\drivers\etc\hosts

## Accédez à l’application :
http://hamza.local

✅ Option B – Accès via port-forwarding
```bash
kubectl port-forward svc/hamza-service 8080:80 -n hamza-project
```
## Puis accédez à :
http://localhost:8080

## 🧰 Vérification & debug
```bash
kubectl get pods -n hamza-project
kubectl get svc -n hamza-project
kubectl logs -f deployment/hamza-app -n hamza-project 
```
### Linux with Minikube
# 🚀 Kubernetes Project: hamza.local Setup Guide (Linux)

This guide explains how to run the project locally on a Linux machine using Minikube, and access the app in your browser via `http://hamza.local`.

---

## ✅ Requirements

- Linux-based system
- Virtualization support (KVM, VirtualBox, etc.)
- Internet connection

---

## 🐳 PARTIE 1 : Installer Docker sur Ubuntu
✅ Étapes :

```bash
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```
🔁 Démarrer Docker et activer au démarrage :
```bash
sudo systemctl enable docker
sudo systemctl start docker
```
Make docker command accessible without sudo:

```bash
sudo usermod -aG docker $USER && newgrp docker
```
📌 Explication :
usermod -aG docker $USER : ajoute ton utilisateur au groupe docker
newgrp docker : recharge les groupes sans redémarrage

### ☸️ PARTIE 2 : Installer Kubernetes avec Minikube
🎯 Pourquoi Minikube ?
Minikube est idéal pour tester Kubernetes en local dans une VM ou une machine virtuelle.

✅ Étapes d'installation :
1. Installer kubectl (outil de gestion Kubernetes)
```bash
sudo apt update
sudo apt install -y curl
curl -LO "https://dl.k8s.io/release/v1.30.1/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```
2. Installer Minikube
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
3. Lancer Minikube avec Docker comme driver
```bash
minikube start --driver=docker
```
✅ Il créera un cluster local
4. Vérifier le fonctionnement
```bash
kubectl get nodes
```
Tu devrais voir un nœud minikube en Ready.

🛠️ Active ces 3 addons dans Minikube :
```bash
minikube addons enable default-storageclass
minikube addons enable storage-provisioner
minikube addons enable ingress
```
📌 Explication :

2 addons first pour Activer le stockage automatique dans Minikube
The last addon for Enable Ingress Controller

## 🧪 Déploiement local avec Kubernetes (Minikube)
In the first we need to clone the repo in the local with this command"
```bash
git clone https://github.com/hamzahssaini/Kubernetes-Project.git
cd Kuberbetes-Project
```
🧱 1. Créer le namespace
```bash
kubectl apply -f k8s/namespace.yaml
```
🗃 2. Déployer MongoDB
```bash
kubectl apply -f dbmongo/
```
🚀 3. Déployer l’application Node.js
```bash
kubectl apply -f k8s/
```
Verification
```bash
kubectl get pods -n hamza-project
```

🖥️   4. Configure Local DNS

Get Minikube IP:
```bash
minikube ip
```
Edit your hosts file:
```bash
sudo nano /etc/hosts
```
Add this line at the bottom:
```bash
<MINIKUBE_IP>    hamza.local
```
🌐  5. Access the App in Browser
Open your browser and go to:

http://hamza.local

📞 Support
If you face issues:
Make sure the pods are running: 
```bash
kubectl get pods -n hamza-project
```
Check Ingress logs: 
```bash
kubectl logs -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx
```
Or contact me sur LinkedIn

👨‍💻 Auteur
Hamza Hssaini
[📎 LinkedIn](https://www.linkedin.com/in/hamza-hssaini-149a9b310)

📜 Licence
Ce projet est open source, vous pouvez le réutiliser, le modifier et le partager à des fins éducatives.
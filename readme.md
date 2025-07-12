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

# 🚀 Kubernetes 3-Tier Deployment for Realtime Chat App

This repository contains Kubernetes manifests to deploy a **3-tier realtime chat application** consisting of:

- 🎨 **Frontend**: React (Vite)  
- 🔧 **Backend**: Node.js (Express)  
- 📂 **Database**: MongoDB  

> 📁 Only the Kubernetes configurations are included in this repository. The source code for the app is assumed to be containerized and hosted in a container registry.

---

## 🧱 Architecture

```
[Frontend (Vite)]
      |
      v
[Service: frontend (ClusterIP)]
      |
      v
[Backend (Express)]
      |
      v
[Service: backend (ClusterIP)]
      |
      v
[MongoDB]
[Service: mongo (ClusterIP)]
```

---

## 📁 Contents

All manifests are located in this directory:

- `frontend-deployment.yaml`  
- `frontend-svc.yaml`  
- `backend-deployment.yaml`  
- `backend-svc.yaml`  
- `mongodb-deployment.yaml`  
- `mongodb-svc.yaml`  
- `pvc.yaml` 
- `pv.yaml`  
- `secrets.yaml`  
- `namespace.yaml`  

---

## 📦 How to Deploy

1. Make sure your Kubernetes cluster is running (Minikube, Docker Desktop, or cloud).
2. Apply the manifests:

   ```bash
   kubectl apply -f kubernetes/
   ```

3. (Optional) If using namespaces, create it first:

   ```bash
   kubectl create namespace chat-app
   ```

4. Forward the frontend service to localhost:

   ```bash
   kubectl port-forward svc/frontend 8080:80 -n chat-app
   ```

5. Visit your app at [http://localhost:8080](http://localhost:8080)

---

## 🔗 Internal Connections

- Backend connects to MongoDB via:  
  `mongodb://mongo:27017/chat-app`
- Frontend talks to backend using:  
  `http://backend:5001` (resolvable within the cluster)

---

## 💾 Data Persistence

MongoDB is backed by a PersistentVolumeClaim, ensuring data is retained even if pods restart.

---

## ⚠️ Notes

This setup is ideal for **development** or **learning** purposes. For production:

- Add Ingress with TLS (e.g. using NGINX or Traefik)  
- Use Kubernetes Secrets for sensitive info  
- Add Liveness & Readiness Probes  
- Configure resource requests & autoscaling  

---

## 📜 License

MIT License — free to use and modify. Contributions welcome! 🤝


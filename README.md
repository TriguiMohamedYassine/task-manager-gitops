# Task Manager — Dépôt GitOps

Ce dépôt contient l'ensemble des manifestes Kubernetes et la configuration Argo CD pour le déploiement continu de l'application **Task Manager**.

## Structure

```text
task-manager-gitops/
├── kubernetes/
│   ├── frontend/
│   │   ├── deployment.yaml
│   │   └── service.yaml
│   ├── backend/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── configmap.yaml
│   └── postgres/
│       ├── statefulset.yaml
│       ├── service.yaml
│       └── pvc.yaml
├── argocd/
│   └── application.yaml
└── README.md
```

## Déploiement manuel sur Minikube (pour tester)

1. Créer le namespace et le secret :
```bash
kubectl create namespace task-manager
kubectl create secret generic postgres-secret --from-literal=postgres-password=postgres -n task-manager
```

2. Appliquer les configurations :
```bash
kubectl apply -f kubernetes/postgres/ -n task-manager
kubectl apply -f kubernetes/backend/ -n task-manager
kubectl apply -f kubernetes/frontend/ -n task-manager
```

3. Accéder à l'application :
```bash
minikube service frontend -n task-manager
```

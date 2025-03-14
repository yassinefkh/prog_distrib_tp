# Déploiement d'un service avec Docker et Kubernetes

## 1. Construction et exécution de l'image Docker

### Compilation du projet Java
```bash
./gradlew build
```
Le fichier `.jar` est généré dans `build/libs`.

### Création de l'image Docker
S'assurer d'avoir un `Dockerfile` dans notre dossier de code, puis exécuter :
```bash
docker build -t rent .
```

### Exécution du conteneur
```bash
docker run -p 4000:8080 rent
```
Puis vérifier dans le navigateur :
```
http://localhost:4000/cars
```

## 2. Publication de l'image sur Docker Hub

### Ajouter un tag à l’image
```bash
docker tag <IMAGE_ID> yassinefkh/rent:1
```

### Connexion à Docker Hub
```bash
docker login
```

### Pousser l’image sur Docker Hub
```bash
docker push yassinefkh/rent:1
```

## 3. Déploiement sur Kubernetes avec Minikube

### Installation de Minikube
[Téléchargez Minikube](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Fx86-64%2Fstable%2Fbinary+download).

### Démarrer Minikube
```bash
minikube start --driver=docker
```

### Vérifier le nombre de nœuds dans le cluster
```bash
kubectl get nodes
```

### Ouvrir le tableau de bord Minikube
```bash
minikube dashboard
```

### Déploiement de l’image sur Kubernetes
```bash
kubectl create deployment rent --image=yassinefkh/rent:1
```

### Vérification du bon fonctionnement du pod
```bash
kubectl get pods
```

### Exposition du service via un LoadBalancer
```bash
kubectl expose deployment rent --type=LoadBalancer --port=8080
```

### Récupération de l’URL du service
```bash
minikube service rent --url
```
Tester dans le navigateur.

## 4. Scaling des pods Kubernetes

### Augmenter le nombre de réplicas à 2
```bash
kubectl scale --replicas=2 deployment/rent
```
Puis vérifier :
```bash
kubectl get pods
```

### Supprimer un pod et observer la recréation automatique
```bash
kubectl delete pod <NOM_DU_POD>
```
Puis surveiller :
```bash
kubectl get pods -w
```

### Réduction des réplicas à 1
```bash
kubectl scale --replicas=1 deployment/rent
```

Ici si on met replicas=2, Kubernetes veut garder 2 pods, donc va recréer un automatiquement si on en supprime un.

## 5. Github Workflows

### Création et passage sur une nouvelle branche
```bash
git branch essai
git checkout essai
```

### Mise à jour et commit des changements
```bash
git commit -a -m "essai"
```

### Retour à la branche principale
```bash
git checkout main
```

### Pousser les changements sur GitHub
```bash
git push -u origin essai
```

### Création d'une Pull Request et fusion sur GitHub
Sur GitHub, on créer une Pull Request et fusionne si tout est correct.

### Récupérer la dernière version principale
```bash
git checkout main
git pull origin main
```



# 🚀 README - Déploiement de PayMyBuddy avec Docker Compose

## Description
Ce guide décrit toutes les étapes nécessaires pour déployer l'application **PayMyBuddy** (Spring Boot + MySQL).

---

## 🔄 1. Prérequis

- [Docker](https://docs.docker.com/get-docker/) installé  
- [Docker Compose](https://docs.docker.com/compose/) installé  
- **Java 17+** si vous voulez recompiler le JAR  

### Vérifiez les versions installées et cloner le projet :
```bash
docker --version
docker compose version
java -version


git clone https://github.com/kingsleyDeve/Mini-projet-docker.git
cd Mini-projet-docker
```

---

## 📂 2. Structure du projet

```
.
├── Dockerfile
├── docker-compose.yml
├── .env
├── initdb/
│   └── create.sql
└── target/
    └── paymybuddy.jar
```

---

## 📝 3. Fichier .env

Créez un fichier `.env` à la racine du projet avec :

```dotenv
MYSQL_DATABASE=db_paymybuddy
MYSQL_USER=USER
MYSQL_PASSWORD=MDP
MYSQL_ROOT_PASSWORD=MDP

SPRING_DATASOURCE_URL=jdbc:mysql://paymybuddy-db:3306/db_paymybuddy
SPRING_DATASOURCE_USERNAME=USER
SPRING_DATASOURCE_PASSWORD=MDP
```

---

## 🐳 4. Lancer l'infrastructure

### Compiler le backend si nécessaire :
```bash
docker build -t paymybuddy-app .

docker build -t paymybuddy-db -f Dockerfile-db .
```

### Démarrer les conteneurs en arrière-plan :
```bash
docker compose up -d
```

### Vérifier les conteneurs en cours :
```bash
docker compose ps
```

### Suivre les logs :
```bash
docker compose logs -f
```

---

## 💻 5. Accès à l'application

- Backend Spring Boot disponible sur : 👉 [http://localhost:8080](http://localhost:8080)  
- Base de données MySQL accessible sur : 👉 `localhost:3306`  

---

## 🔧 6. Commandes utiles

Recompiler le backend si le code change (optionnel) :
```bash

docker build -t paymybuddy-app .
```

Relancer avec la nouvelle image :
```bash
docker compose up -d --build
```

Supprimer les conteneurs et volumes (reset complet) :
```bash
docker compose down -v
```

---

## 🌍 7. Architecture

- **Utilisateur** → **Backend (Spring Boot)** → **MySQL**  
- MySQL est initialisé au premier lancement via `initdb/create.sql`  
- Les données sont persistées dans le volume **paymybuddy-data**

##  8. Création des images dans un repository public 

```bash
docker tag paymybuddy-db kingsley95/mini-projet-docker:paymybuddy-db
docker push kingsley95/mini-projet-docker:paymybuddy-db

docker tag paymybuddy-app kingsley95/mini-projet-docker:paymybuddy-app
docker push kingsley95/mini-projet-docker:paymybuddy-app
```
---

✅ Déploiement terminé !

Image du résultat présent dans le dossier img 

**![PayMyBuddy Overview](https://github.com/kingsleyDeve/Mini-projet-docker/blob/main/img/accueil.PNG)**


**![PayMyBuddy Accueil Overview](https://github.com/kingsleyDeve/Mini-projet-docker/blob/main/img/connecter.PNG)**


**![PayMyBuddy SQL Overview](https://github.com/kingsleyDeve/Mini-projet-docker/blob/main/img/sql.PNG)**

**![PayMyBuddy dockerhub Overview](https://github.com/kingsleyDeve/Mini-projet-docker/blob/main/img/hub.PNG)**

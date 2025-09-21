#!/bin/bash
# ==========================================================
# 🚀 README - Déploiement de PayMyBuddy avec Docker Compose
# ==========================================================

# Description :
# Ce script décrit toutes les étapes nécessaires pour
# déployer l'application PayMyBuddy (Spring Boot + MySQL).
# ==========================================================


# ----------------------------------------
# 🔄 1. Prérequis
# ----------------------------------------
# - Docker installé : https://docs.docker.com/get-docker/
# - Docker Compose installé : https://docs.docker.com/compose/
# - Java 17+ si vous voulez recompiler le JAR
# ----------------------------------------

# Vérifiez les versions installées :
docker --version
docker compose version
java -version

# ----------------------------------------
# 📂 2. Structure du projet
# ----------------------------------------
# .
# ├── Dockerfile
# ├── docker-compose.yml
# ├── .env
# ├── initdb/
# │   └── create.sql
# └── target/
#     └── paymybuddy.jar
# ----------------------------------------

# ----------------------------------------
# 📝 3. Fichier .env
# ----------------------------------------
# Créez un fichier .env à la racine du projet avec :
cat > .env <<EOF
MYSQL_DATABASE=db_paymybuddy
MYSQL_USER=USER
MYSQL_PASSWORD=MDP
MYSQL_ROOT_PASSWORD=MDP

SPRING_DATASOURCE_URL=URL
SPRING_DATASOURCE_USERNAME=USER
SPRING_DATASOURCE_PASSWORD=MDP
EOF

# ----------------------------------------
# 🐳 4. Lancer l'infrastructure
# ----------------------------------------

# Compiler le backend si nécessaire
docker build -t paymybuddy-app .

# Démarrer les conteneurs en arrière-plan
docker compose up -d

# Vérifier les conteneurs en cours
docker compose ps

# Suivre les logs
docker compose logs -f

# ----------------------------------------
# 💻 5. Accès à l'application
# ----------------------------------------
# Backend Spring Boot disponible sur :
# 👉 http://localhost:8080
#
# Base de données MySQL accessible sur :
# 👉 localhost:3306
# ----------------------------------------

# ----------------------------------------
# 🔧 6. Commandes utiles
# ----------------------------------------

# Recompiler le backend si le code change
mvn clean package -DskipTests
docker build -t paymybuddy-app .

# Relancer avec nouvelle image
docker compose up -d --build

# Supprimer les conteneurs et volumes (reset complet)
docker compose down -v

# ----------------------------------------
# 🌍 7. Architecture
# ----------------------------------------
# Utilisateur -> Backend (Spring Boot) -> MySQL
# MySQL est initialisé au premier lancement via initdb/create.sql
# Les données sont persistées dans le volume paymybuddy-data
# ----------------------------------------

# ==========================================================
# ✅ Déploiement terminé !
# ==========================================================


img/accueil.PNG


img/connecter.PNG

img/sql.PNG
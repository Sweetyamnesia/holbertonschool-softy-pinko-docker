# 🐳 Docker — Guide d’introduction

Docker est une plateforme open-source qui permet de **créer, déployer et exécuter des applications** dans des **conteneurs**.  
Les conteneurs sont des environnements légers, portables et isolés qui embarquent tout le nécessaire pour faire fonctionner une application : **code, bibliothèques, dépendances et configuration**.

---

## 📌 Sommaire

- [Qu’est-ce que Docker ?](#-quest-ce-que-docker-)
- [Pourquoi utiliser Docker ?](#-pourquoi-utiliser-docker-)
- [Installation de Docker](#-installation-de-docker)
- [Commandes de base](#-commandes-de-base)
- [Dockerfile et images personnalisées](#-dockerfile-et-images-personnalisées)
- [Docker Compose](#-docker-compose)
- [Bonnes pratiques](#-bonnes-pratiques)
- [Ressources utiles](#-ressources-utiles)

---

## 🐋 Qu’est-ce que Docker ?

Docker est un outil qui permet d’emballer une application et ses dépendances dans un **conteneur**.  
Contrairement aux machines virtuelles, les conteneurs partagent le même **noyau** que l’hôte, ce qui les rend **plus rapides, plus légers et plus efficaces**.

---

## 🚀 Pourquoi utiliser Docker ?

- **Portabilité** : un conteneur peut tourner sur n’importe quelle machine.
- **Isolation** : chaque conteneur fonctionne indépendamment.
- **Cohérence** : "ça marche sur ma machine" → ça marchera partout.
- **Scalabilité** : déployer rapidement plusieurs instances.
- **Facilité d’intégration CI/CD** : parfait pour les pipelines DevOps.

---

## 🛠 Installation de Docker

### Sous Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

### Sous macOS et Windows

Téléchargez **Docker Desktop** depuis le site officiel :  
🔗 https://www.docker.com/products/docker-desktop

---

## 📦 Commandes de base

| Commande               | Description                               |
|-----------------------|-------------------------------------------|
| `docker --version`    | Vérifie la version installée             |
| `docker pull <image>` | Télécharge une image                     |
| `docker images`       | Liste les images disponibles            |
| `docker run <image>`  | Lance un conteneur à partir d’une image |
| `docker ps`          | Affiche les conteneurs en cours         |
| `docker stop <id>`   | Arrête un conteneur                      |
| `docker rm <id>`     | Supprime un conteneur                   |
| `docker rmi <image>` | Supprime une image                      |

---

## 📝 Dockerfile et images personnalisées

Un **Dockerfile** est un fichier texte qui décrit **comment construire une image Docker**.  
Exemple simple :

```dockerfile
# Utiliser une image de base officielle
FROM node:18

# Définir le dossier de travail
WORKDIR /app

# Copier les fichiers dans le conteneur
COPY . .

# Installer les dépendances
RUN npm install

# Exposer le port
EXPOSE 3000

# Lancer l'application
CMD ["npm", "start"]
```

Pour construire et lancer l’image :

```bash
docker build -t mon-app .
docker run -p 3000:3000 mon-app
```

---

## 🧩 Docker Compose

**Docker Compose** permet de gérer plusieurs conteneurs via un seul fichier `docker-compose.yml`.  
Exemple :

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app
    depends_on:
      - db
  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
```

Pour lancer les services :

```bash
docker-compose up -d
```

---

## ✅ Bonnes pratiques

- Utiliser des **images légères** (`alpine`, `slim`…)
- Éviter de stocker des secrets dans les Dockerfiles
- Utiliser `.dockerignore` pour éviter d’envoyer des fichiers inutiles
- Nettoyer régulièrement les images et conteneurs :

```bash
docker system prune -a
```

---

## 📚 Ressources utiles

- [Documentation officielle Docker](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/) — Images officielles
- [Docker Compose](https://docs.docker.com/compose/)

---

💡 **Astuce :** Combinez Docker avec **Docker Compose** pour des environnements de développement complets et reproductibles.


🚀 Mboa-Test: CI/CD Pipeline Automatisé avec Jenkins et Docker
📌 Description
Ce projet met en place un pipeline CI/CD avec Jenkins, qui permet de :
✅ Cloner un dépôt GitHub et récupérer le code source
✅ Effectuer une analyse de code avec SonarQube (qualité du code)
✅ Construire et pousser une image Docker sur DockerHub
✅ Déployer l'application sur un serveur distant via SSH
✅ Nettoyer automatiquement le serveur après utilisation pour optimiser les coûts

🛠️ Technologies utilisées
🔹 Jenkins 🛠️ - Automatisation des pipelines CI/CD
🔹 Docker 🐳 - Conteneurisation de l’application
🔹 SonarQube 🔍 - Analyse statique du code
🔹 SSH & DockerHub 🌐 - Déploiement et gestion des conteneurs à distance

🚀 Comment l’utiliser ?
1️⃣ Cloner le repo
bash
Copy
Edit
git clone https://github.com/AlbanE237/mboa-test.git
cd mboa-test
2️⃣ Configurer Jenkins
Ajouter les credentials nécessaires (GitHub, DockerHub, SSH).

Configurer un nouveau pipeline en important le Jenkinsfile.

3️⃣ Exécuter le pipeline
Déclencher le build via Jenkins.

Vérifier l’analyse de code et la construction du conteneur Docker.

Le pipeline déploiera automatiquement l’application et nettoiera le serveur.

📂 Structure du projet
scss
Copy
Edit
📦 mboa-test
 ┣ 📂 docker
 ┃ ┗ 📜 Dockerfile
 ┣ 📂 jenkins
 ┃ ┗ 📜 Jenkinsfile
 ┣ 📂 scripts
 ┃ ┗ 📜 deploy.sh  (à venir)
 ┣ 📂 docs
 ┃ ┗ 📜 README.md
 ┗ 📜 .gitignore
🤝 Contribution
🚀 Toute contribution est la bienvenue !

Fork le projet 🍴

Crée une branche feature-xxx 🌱

Apporte tes modifications et fais un commit 💡

Ouvre une PR (Pull Request) 🚀

📞 Contact
👤 Alban
📧 LinkedIn

⭐ Si ce projet t’a aidé, n’hésite pas à laisser un ⭐ sur le repo !

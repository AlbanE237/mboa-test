 Mboa-Test: Automated Apache Server Deployment CI/CD Pipeline with Jenkins and Docker

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)

📌 Description

⚡ This project automates the deployment of an Apache server using Jenkins, Docker, and GitHub Actions for Docker validation .

This project sets up a CI/CD pipeline using Jenkins, which allows:

✅ Cloning a GitHub repository and retrieving the source code

✅ Performing code analysis with SonarQube (code quality)

✅ Building and pushing a Docker image to DockerHub

✅ Deploying the application to a remote server via SSH

✅ Automatically cleaning up the server after deployment to optimize costs

🛠️ Technologies Used


🔹 Jenkins & Github action 🛠️ - CI/CD pipeline automation

🔹 Docker 🐳 - Application containerization

🔹 SonarQube 🔍 - Static code analysis

🔹 SSH & DockerHub 🌐 - Remote deployment and container management

 Prerequisites

Before you begin, make sure you have installed:

Docker 🐳 → [Installation](https://docs.docker.com/get-docker/)

Jenkins 🛠️ → [Installation](https://www.jenkins.io/doc/book/installing/)

SonarQube 🔍 (optional, for code analysis)  


 How to Use?

1️⃣ Clone the Repository

 - git clone https://github.com/AlbanE237/mboa-test.git

 - cd mboa-test

2️⃣ Set Up Jenkins

- Add the required credentials (GitHub, DockerHub, SSH)
- Configure a new pipeline by importing the Jenkinsfile

3️⃣ Run the Pipeline

- Trigger the build via Jenkins
- Verify the code analysis and Docker container build
- The pipeline will automatically deploy the application and clean up the server if stage check box On

⚙️ Server Update Before Deployment

Before deploying Apache, the remote server (a VM on Google Cloud Platform) is automatically updated using `apt update`.

Keeping the server updated ensures:

- Better security by applying the latest patches.
- Improved stability by using the most recent versions of system packages.
- Prevention of potential issues during Docker deployment.

This good practice strengthens the reliability and security of the deployed application.


📂 Project Structure

📦 mboa-test

┣ 📂 .github
┃ ┗ 📂 workflows
┃   ┗ 📜 ci-pipeline.yml            # GitHub Actions workflow

┣ 📂 inance                         # Static web files for the container

┣ 📜 Dockerfile                     # Docker build instructions

┣ 📜 Jenkinsfile                    # Jenkins pipeline configuration

┣ 📜 README.md                      # Project documentation

┣ 📜 .gitignore                     # Ignored files and folders

┣ 📜 CONTRIBUTING.md               # Guidelines for contributing

┣ 📜 CODE_OF_CONDUCT.md            # Contributor code of conduct

┣ 📜 SECURITY.md                   # Security policy

┗ 📜 LICENSE                        # MIT License



📈 Status
---------

✅ The project is complete and the deployment is fully automated.


## 🔗 Connect with me

- [LinkedIn](https://www.linkedin.com/in/alban-eboua-9b4510140/?locale=en_US)
- [GitHub](https://github.com/AlbanE237)

⭐ If this project helps you, don't forget to leave a ⭐ on the repo!


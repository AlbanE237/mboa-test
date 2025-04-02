🚀 Mboa-Test: Automated CI/CD Pipeline with Jenkins and Docker

📌 Description


This project sets up a CI/CD pipeline using Jenkins, which allows:

✅ Cloning a GitHub repository and retrieving the source code

✅ Performing code analysis with SonarQube (code quality)

✅ Building and pushing a Docker image to DockerHub

✅ Deploying the application to a remote server via SSH

✅ Automatically cleaning up the server after deployment to optimize costs

🛠️ Technologies Used


🔹 Jenkins 🛠️ - CI/CD pipeline automation

🔹 Docker 🐳 - Application containerization

🔹 SonarQube 🔍 - Static code analysis

🔹 SSH & DockerHub 🌐 - Remote deployment and container management


🚀 How to Use?

1️⃣ Clone the Repository

git clone https://github.com/AlbanE237/mboa-test.git

cd mboa-test

2️⃣ Set Up Jenkins

Add the required credentials (GitHub, DockerHub, SSH)

Configure a new pipeline by importing the Jenkinsfile

3️⃣ Run the Pipeline

Trigger the build via Jenkins

Verify the code analysis and Docker container build

The pipeline will automatically deploy the application and clean up the server if stage check box On

📂 Project Structure

📦 mboa-test

 ┣ 📂 docker
 ┃ ┗ 📜 Dockerfile
 
 ┣ 📂 jenkins
 ┃ ┗ 📜 Jenkinsfile
 
 ┣ 📂 scripts
 ┃ ┗ 📜 deploy.sh  (coming soon)
 
 ┣ 📂 docs
 ┃ ┗ 📜 README.md
 
 ┗ 📜 .gitignore


🤝 Contributing

🚀 Contributions are welcome!

Fork the project 🍴

Create a new branch feature-xxx 🌱

Make your changes and commit 💡

Open a PR (Pull Request) 🚀

📞 Contact

👤 Alban Eboua

📧 [LinkedIn](https://www.linkedin.com/in/albaneboua/)

⭐ If this project helps you, don't forget to leave a ⭐ on the repo!


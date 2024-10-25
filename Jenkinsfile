pipeline {
    agent any

    parameters {
        string(name: 'github-url', defaultValue: '', description: 'Enter your GitHub URL')
        string(name: 'image-name', defaultValue: 'dockerhubusername/repo-name', description: 'Enter your image name')
        string(name: 'image-tag', defaultValue: '', description: 'Enter your image tag')
    }

    environment {
        scanner = tool 'sonar'
    }

    stages {
        stage("Checkout Code") {
            steps {
                git branch: 'main', url: "${params['github-url']}", credentialsId: "alban-github-token"
            }
        }
        stage("Code Scan") {
            steps {
                script {
                    withCredentials([string(credentialsId: 'sonar', variable: 'SONAR_TOKEN')]) {
                        withSonarQubeEnv('sonar') {
                            sh '''
                            $scanner/bin/sonar-scanner \
                            -Dsonar.login=$SONAR_TOKEN \
                            -Dsonar.host.url=http://18.219.90.216:9000/ \
                            -Dsonar.projectKey=alban \
                            -Dsonar.sources=./mboa-test
                            '''
                        }
                    }
                }
            }
        }
        stage("Build Dockerfile") {
            steps {
                script {
                    sh "docker build -t ${params['image-name']}:${params['image-tag']} ."
                }
            }
        }
        stage("Connect to DockerHub") {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "alban_dockerhub-credential", passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                        sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                    }
                }
            }
        }
        stage("Push to DockerHub") {
            steps {
                script {
                    sh "docker push ${params['image-name']}:${params['image-tag']}"
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
pipeline {
    agent any

    parameters {
        string(name: 'github-url', defaultValue: '', description: 'Enter your GitHub URL')
        string(name: 'image-name', defaultValue: 'dockerhubusername/repo-name', description: 'Enter your image name')
        string(name: 'image-tag', defaultValue: '', description: 'Enter your image tag')
        booleanParam(name: 'skip', defaultValue: false, description: "Mark for yes or leave empty for false")
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
                            -Dsonar.host.url=http://http://18.216.0.51:9000// \
                            -Dsonar.projectKey=alban \
                            -Dsonar.sources=./inance
                            '''
                        }
                    }
                }
            }
        }
        stage("Build Dockerfile") {
            when {
                expression { !params.skip } // Only execute if 'skip' is false
            }
            steps {
                script {
                    sh "docker build -t ${params['image-name']}:${params['image-tag']} ."
                }
            }
        }
        stage("Connect to DockerHub") {
            when {
                expression { !params.skip } // Only execute if 'skip' is false
            }
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "alban_dockerhub-credential", passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                        sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                    }
                }
            }
        }
        stage("Push to DockerHub") {
            when {
                expression { !params.skip } // Only execute if 'skip' is false
            }
            steps {
                script {
                    sh "docker push ${params['image-name']}:${params['image-tag']}"
                }
            }
        }
        stage("Remove All Docker Images") {
            steps {
                script {
                    sh '''
                    docker rmi $(docker images -q) || true
                    '''
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

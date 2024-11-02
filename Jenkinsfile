pipeline {
    agent any

    parameters {
        string(name: 'github-url', defaultValue: '', description: 'Enter your GitHub URL')
        string(name: 'image-name', defaultValue: 'dockerhubusername/repo-name', description: 'Enter your image name')
        string(name: 'image-tag', defaultValue: '', description: 'Enter your image tag')
        string(name: 'password', defaultValue: '', description: 'Enter your password for remote server')
        string(name: 'remote_user', defaultValue: '', description: 'Enter your remote user')
        string(name: 'server_dns', defaultValue: '', description: 'Enter your server DNS')
        booleanParam(name: 'skip', defaultValue: false, description: "Pour Skip Code scan, build to Push")
        booleanParam(name: 'skip_deployment', defaultValue: false, description: 'Pour Skip le Deployment')
        booleanParam(name: 'clean_deployment', defaultValue: false, description: 'Pour Clean le serveur du déploiement')
    }

    environment {
        scanner = tool 'sonar'
    }

    stages {
        stage("Clone repository") {
            steps {
                git branch: 'main', url: "${params['github-url']}", credentialsId: "alban-github-token"
            }
        }
        stage("Code scan") {
            when {
                expression { !params.skip }  // cocher "skip" pour sauter ce stage
            }
            steps {
                script {
                    withCredentials([string(credentialsId: 'sonar', variable: 'SONAR_TOKEN')]) {
                        withSonarQubeEnv('sonar') {
                            sh '''
                            $scanner/bin/sonar-scanner \
                            -Dsonar.login=$SONAR_TOKEN \
                            -Dsonar.host.url=http://3.17.190.122:9000/ \
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
                expression { !params.skip }  // cocher "skip" pour sauter ce stage
            }
            steps {
                script {
                    sh "docker build -t ${params['image-name']}:${params['image-tag']} ."
                }
            }
        }
        stage("Connect to DockerHub") {
            when {
                expression { !params.skip }  // cocher "skip" pour sauter ce stage
            }
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "alban_dockerhub-credential", 
                    usernameVariable: "DOCKER_USERNAME", passwordVariable: "DOCKER_PASSWORD")]) {
                        sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                    }
                }
            }
        }
        stage("Push to DockerHub") {
            when {
                expression { !params.skip }  // cocher "skip" pour sauter ce stage
            }
            steps {
                script {
                    sh "docker push ${params['image-name']}:${params['image-tag']}"
                }
            }
        }
        stage("Connect to remote and deploy") {
            when {
                expression { !params.skip_deployment }  // cocher "skip_deployment" pour sauter ce stage
            }
            steps {
                script {
                    sh "sshpass -p '${params['password']}' ssh -o StrictHostKeyChecking=no ${params['remote_user']}@${params['server_dns']} 'docker run -itd --name mboa-test -p 8086:80 ${params['image-name']}:${params['image-tag']}'"
                }
            }
        }
        stage("Clean deployment server") {
            when {
                expression { params.clean_deployment } // Cocher pour activer ce stage de "Clean"
            }
            steps {
                script {
                    sh """
                    sshpass -p '${params['password']}' ssh -o StrictHostKeyChecking=no ${params['remote_user']}@${params['server_dns']} '
                        if [ \$(docker ps -q) ]; then
                            docker stop \$(docker ps -q) && docker rm \$(docker ps -q)
                        fi
                        if [ \$(docker images -q) ]; then
                            docker rmi -f \$(docker images -q)
                        fi
                    '
                    """
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

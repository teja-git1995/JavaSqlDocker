pipeline {
    agent any

    tools {
    maven 'TejaMVN'
}
    environment {
        WORKSPACE = "/var/lib/jenkins/workspace/Project"
        DOCKER_IMAGE = "myapp-backend:1.0"
        REGISTRY = "teja072/myapp-backend"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/teja-git1995/JavaSqlDocker.git'
            }
        }

        stage('Build') {
            steps {
                sh 'cd ${WORKSPACE}/backend && mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "cd ${WORKSPACE}/backend && docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Push to Registry') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-cred', url: '']) {
                    sh "docker tag ${DOCKER_IMAGE} ${REGISTRY}:latest"
                    sh "docker push ${REGISTRY}:latest"
                }
            }
        }

        stage('Deploy to Swarm') {
            steps {
                sh """
                    docker service update --image ${REGISTRY}:latest backend || \
                    docker service create --name backend --replicas 3 --publish 8081:8081 ${REGISTRY}:latest
                """
            }
        }
    }
}

pipeline {
    agent any
    environment {
        DOCKER_HUB_USERNAME = credentials('docker-hub-creds').username
        DOCKER_HUB_PASSWORD = credentials('docker-hub-creds').password
    }
    stages {
        stage('Clone Step') {
            steps {
                sh 'rm -rf hello-world-war'
                sh 'git clone https://github.com/prasanthplavada/hello-world-war.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mvn_docker .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                    sh 'docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'
                    sh 'docker tag mvn_docker $DOCKER_HUB_USERNAME/mvn_docker:$BUILD_NUMBER'
                    sh 'docker push $DOCKER_HUB_USERNAME/mvn_docker:$BUILD_NUMBER'
                }
            }
        }
        stage('Deploy Step') {
            steps {
                sh 'docker run -itd -p 8090:8080 --name tom_docker mvn_docker'
                sh 'docker rm -f tom_docker'
            }
        }
    }
}

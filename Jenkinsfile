pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mvn_docker .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry([ credentialsId: "docker-hub-creds", url:""]) {
                    sh 'docker tag mvn_docker vikas2609/mvn_docker:$BUILD_NUMBER'
                    sh 'docker push vikas2609/mvn_docker:$BUILD_NUMBER' 
                }
            }
        }
        stage('Deploy Step') {
            steps {
                withDockerRegistry([ credentialsId: "docker-hub-creds", url:""]) {
                 sh 'docker pull vikas2609/mvn_docker:$BUILD_NUMBER'
                }
                sh 'docker rm -f tom_docker'
                sh 'docker run -itd -p 8070:8080 --name tom_docker vikas2609/mvn_docker:$BUILD_NUMBER'
            }
        }
    }
}

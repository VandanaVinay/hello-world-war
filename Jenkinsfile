pipeline {
    agent {
        label "deploy"
    }
    stages {
        stage('Tomcat_install') {
            steps {
                sh 'rm -rf hello-world-war'
                sh 'git clone https://github.com/Vikas2609/hello-world-war.git'
                sh 'chmod 755 ${workspace}/hello-world-war/tomcat_install'
                sh '${workspace}/hello-world-war/tomcat_install'
            }
        }
//         stage('clone step') {
//             steps {
//                 sh 'rm -rf hello-world-war'
//                 sh 'git clone https://github.com/Vikas2609/hello-world-war.git'
//             }
//         }
        stage('Build') {
            steps {
                dir('hello-world-war'){
                sh 'mvn package'
                }
            }
        }
        stage('Deploy step') {
            steps {
                sh 'sudo cp ${WORKSPACE}/target/hello-world-war-1.0.0.war /var/lib/tomcat9/webapps'       
            }
        }
    }
}

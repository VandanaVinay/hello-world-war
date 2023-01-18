pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/apache-maven/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git 'https://github.com/dptrealtime/java-login-app.git'
            }
         }
       stage('mvn clean package'){
            steps{
                sh 'mvn clean package'
            }
        }
       stage('mvn clean install'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('mvn test'){
            steps{
                sh 'mvn test'
            }
        }
       stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv('sonarqube-8.3.1') { 
                sh ''' mvn verify sonar:sonar -Dsonar.login=admin -Dsonar.password=admin'''
                }
                
            }
        }
       
    }
}

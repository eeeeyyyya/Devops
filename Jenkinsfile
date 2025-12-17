pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonarqube-token', variable: 'SONAR_TOKEN')]) {
                    sh "mvn sonar:sonar -Dsonar.projectKey=devops -Dsonar.host.url=http://localhost:9000 -Dsonar.login=\$SONAR_TOKEN"
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
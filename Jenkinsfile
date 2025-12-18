pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Compilation') {
            steps {
                sh './gradlew -Dhttps.proxyHost=proxy1-rech.uphf.fr -Dhttps.proxyPort=3128 compileJava'
            }
        }
        /*stage('Tests') {
            steps {
                sh './gradlew -Dhttps.proxyHost=proxy1-rech.uphf.fr -Dhttps.proxyPort=3128 test'
            }
        }*/
        stage('Sonar') {
            steps {
                withSonarQubeEnv(installationName: 'sonar'){
                    sh './gradlew sonar -Dsonar.projectKey=TPControl -Dsonar.projectName='TPControl' -Dsonar.host.url=http://localhost:9000 -Dsonar.token=sqp_9fbba9144cc9fa3ac943ac6f6da55a00053cd299'
               }
            }
        }
        stage('Final build') {
            steps {
                sh './gradlew -Dhttps.proxyHost=proxy1-rech.uphf.fr -Dhttps.proxyPort=3128 jar'
            }
        }
    }
}

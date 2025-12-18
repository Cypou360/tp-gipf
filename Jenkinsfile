pipeline {
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Tests') {
            steps {
            }
        }
        stage('Final build') {
            steps {
                sh './gradlew jar'
            }
        }
    }
}

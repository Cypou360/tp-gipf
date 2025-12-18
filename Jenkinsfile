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
        stage('Tests') {
            steps {
                sh './gradlew -Dhttps.proxyHost=proxy1-rech.uphf.fr -Dhttps.proxyPort=3128 test'
            }
        }
        stage('Sonar') {
            steps {
                withSonarQubeEnv(installationName: 'sonar'){
                    sh "./gradlew -Dhttps.proxyHost=proxy1-rech.uphf.fr -Dhttps.proxyPort=3128 sonar -Dsonar.token=squ_6b585d7835b08a3e26a6ee7cc8a922c33ee6f0b4"
               }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES')
                {
                    waitForQualityGate abortPipeline: true
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

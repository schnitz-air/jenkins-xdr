pipeline {
    agent any
    environment {
        CODECOV_TOKEN = credentials('codecov-token') // Make sure this credential is set in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/schnitz-air/jenkins-xdr.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install || true'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
        stage('Upload Coverage to Codecov') {
            steps {
                script {
                    sh 'bash <(curl -s https://codecov.io/bash) -t ${CODECOV_TOKEN}' 
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

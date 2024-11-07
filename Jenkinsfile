pipeline {
    agent any
    environment {
        CODECOV_TOKEN = credentials('codecov-token') // Add your Codecov token to Jenkins credentials
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/schnitz-air/jenkins-xdr.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install' // Adjust according to your package manager
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test' // Run tests and generate coverage report
            }
        }
        stage('Upload Coverage to Codecov') {
            steps {
                sh 'bash <(curl -s https://codecov.io/bash)' 
            }
        }
    }
    post {
        always {
            cleanWs() // Clean the workspace after build
        }
    }
}

pipeline {
    agent any
    environment {
        CODECOV_TOKEN = credentials('codecov-token')
    }
    tools {
        python 'Python 3.8' // Ensure you have added Python installation in Jenkins -> Configure Tools
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/schnitz-air/jenkins-xdr.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'python -m pip install --upgrade pip'
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }
        stage('Upload Coverage to Codecov') {
            steps {
                sh 'bash <(curl -s https://codecov.io/bash) -t ${CODECOV_TOKEN}'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}

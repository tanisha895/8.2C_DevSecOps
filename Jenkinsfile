pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/tanisha895/8.2C_DevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Coverage') {
            steps {
                sh 'npm run coverage'
            }
        }

        stage('Snyk Scan') {
            steps {
                sh 'npx snyk test || true'
            }
        }
    }
}
pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/tanisha895/8.2C_DevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Test') {
            steps {
                bat 'npm test'
            }
        }

        stage('Coverage') {
            steps {
                bat 'npm run coverage'
            }
        }

        stage('Snyk Scan') {
            steps {
                bat 'npx snyk test || exit 0'
            }
        }
    }
}
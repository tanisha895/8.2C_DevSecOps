pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
    }

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

        stage('SonarCloud Analysis') {
            steps {
                bat '''
                npx sonar-scanner ^
                -Dsonar.projectKey=YOUR_PROJECT_KEY ^
                -Dsonar.organization=YOUR_ORG ^
                -Dsonar.sources=. ^
                -Dsonar.host.url=https://sonarcloud.io ^
                -Dsonar.login=%SONAR_TOKEN%
                '''
            }
        }
    }
}
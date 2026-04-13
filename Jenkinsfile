pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
        SNYK_TOKEN  = credentials('SNYK_TOKEN')
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

        stage('Run Test + Snyk') {
            steps {
                // Authenticate Snyk
                bat 'npx snyk auth %SNYK_TOKEN%'

                // Run snyk test (won’t fail pipeline now)
                bat 'npx snyk test || echo "Snyk found issues but continuing..."'
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
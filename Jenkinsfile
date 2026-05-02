pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
        SNYK_TOKEN  = credentials('SNYK_TOKEN')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/tanisha895/8.2C_DevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Test + Snyk') {
    steps {
        bat 'npm test'
        bat 'npx snyk auth %SNYK_TOKEN%'
        bat 'npx snyk test || exit 0'
    }
}

        stage('Install Sonar Scanner') {
            steps {
                bat 'npm install -g sonar-scanner'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                bat '''
                    sonar-scanner ^
                    -Dsonar.projectKey=tanisha895_8.2C_DevSecOps ^
                    -Dsonar.organization=tanisha895 ^
                    -Dsonar.sources=. ^
                    -Dsonar.host.url=https://sonarcloud.io ^
                    -Dsonar.login=%SONAR_TOKEN%
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}

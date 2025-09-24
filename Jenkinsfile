pipeline {
    agent any

    // Ensure Jenkins can find Node.js
    environment {
        PATH = "/opt/homebrew/opt/node@18/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/michaelmorks/8.1CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }
    }

    post {
        always {
            emailext(
                to: 'Michaelmorks30@gmail.com',
                subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - ${currentBuild.currentResult}!",
                body: """Build Status: ${currentBuild.currentResult}

Check console output at ${env.BUILD_URL} to view the results.""",
                attachLog: true
            )
        }
    }
}


pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { git branch: 'main', url: 'https://github.com/michaelmorks/8.1CDevSecOps.git' }
        }
        stage('Install Dependencies') {
            steps { sh 'npm install' }
        }
        stage('Run Tests') {
            steps { sh 'npm test || true' }
        }
        stage('Generate Coverage Report') {
            steps { sh 'npm run coverage || true' }
        }
        stage('NPM Audit (Security Scan)') {
            steps { sh 'npm audit || true' }
        }
    }
    post {
        always {
            emailext(
                to: 'Michaelmorks30@gmail.com',
                subject: "$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!",
                body: """Build Status: $BUILD_STATUS

Check console output at $BUILD_URL to view the results.""",
                attachLog: true
            )
        }
    }
}


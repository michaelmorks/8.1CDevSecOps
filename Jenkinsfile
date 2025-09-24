pipeline {
    agent any
    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/yourusername/8.2CDevSecOps.git'
            }
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
        stage('SonarCloud Analysis') {
            steps {
                sh '''
                # Download SonarScanner CLI
                curl -Lo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.2.2856-macosx.zip
                unzip sonar-scanner.zip
                ./sonar-scanner-4.8.2.2856-macosx/bin/sonar-scanner
                '''
            }
        }
    }
    post {
        always {
            emailext(
                to: 'Michaelmorks30@gmail.com',
                subject: "$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!",
                body: "Check console output at $BUILD_URL to view results."
            )
        }
    }
}

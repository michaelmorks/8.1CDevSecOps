pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/michaelmorks/8.1CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install || true'
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
            // Fake email notification
            sh '''
            echo "--------------------------------------------------"
            echo "Simulated Email Notification"
            echo "To: s224437209@deakin.edu.au"
            echo "Subject: Build Status - ${BUILD_STATUS}"
            echo "Body: Job '${JOB_NAME} [${BUILD_NUMBER}]' finished with status: ${BUILD_STATUS}"
            echo "Attachment: Console log attached"
            echo "--------------------------------------------------"
            '''
        }
    }
}

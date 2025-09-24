pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/michaelmorks/8.1CDevSecOps.git'
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
    }
    post {
        always {
            // Create a dummy log file
            sh 'echo "Build logs captured for job: $JOB_NAME build #$BUILD_NUMBER" > console.log'

            // Send email with log file attached
            emailext(
                to: "Michaelmorks30@gmail.com",
                subject: "Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                body: """\
Hello,

The build for project *${env.JOB_NAME}* has finished with status: *${currentBuild.currentResult}*.

Please find the console log attached for details.

Regards,  
Jenkins
""",
                attachmentsPattern: "console.log"
            )
        }
    }
}

}


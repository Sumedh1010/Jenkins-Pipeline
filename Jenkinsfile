pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'medicala.sumedh@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Initiating the build process...'
            }
        }
        
        stage('Run Tests') {
            steps {
                echo 'Executing Unit Tests and Integration Tests...'
            }
            post {
                always {
                    emailext(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "Test Results: Unit and Integration - ${currentBuild.currentResult}",
                        body: """Unit and Integration Test results: ${currentBuild.currentResult}.
                                 View more details here: ${env.BUILD_URL}.
                                 Check the attached logs for further information.""",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
        
        stage('Code Quality Analysis') {
            steps {
                echo 'Analyzing code quality...'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Conducting security scans...'
            }
            post {
                always {
                    emailext(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "Security Scan Results: ${currentBuild.currentResult}",
                        body: """The security check finished with status: ${currentBuild.currentResult}.
                                 Build details: ${env.BUILD_URL}.
                                 Please find the logs attached.""",
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
        
        stage('Deploy to Staging Environment') {
            steps {
                echo 'Deploying application to the staging environment...'
            }
        }
        
        stage('Test in Staging') {
            steps {
                echo 'Executing tests in the staging environment...'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to the production environment...'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
        always {
            cleanWs() // Clean up workspace after execution
        }
    }
}

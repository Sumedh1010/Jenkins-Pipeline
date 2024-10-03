pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = ‘medicala.sumedh.10@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit Tests and Integration Tests...'
            }
            post {
                always {
                    mail to: "${env.EMAIL_RECIPIENT}",
                         subject: "Unit and Integration Test Stage: ${currentBuild.currentResult}",
                         body: "The Unit and Integration Test stage has ${currentBuild.currentResult}. Please find the attached logs.",
                         attachLog: true
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
            }
            post {
                always {
                    mail to: "${env.EMAIL_RECIPIENT}",
                         subject: "Security Scan Stage: ${currentBuild.currentResult}",
                         body: "The Security Scan stage has ${currentBuild.currentResult}. Please find the attached logs.",
                         attachLog: true
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
            }
        }
    }
    
    post {
    always {
        echo 'Sending basic email notification...'
        emailext (
            subject: "Jenkins Pipeline: ${currentBuild.fullDisplayName}",
            body: """<p>Pipeline completed with status: ${currentBuild.currentResult}</p>
                     <p>Build URL: ${env.BUILD_URL}</p>""",
            to: 'medicala.sumedh.10@gmail.com'  // Replaced curly quotes with straight quotes
        )
    }
}

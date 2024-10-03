pipeline {
    agent any

    environment {
        EMAIL = 'medicala.sumedh.10@gmail.com'
    }

    stages {
        stage('Build Stage') {
            steps {
                echo 'Starting the build process...'
            }
        }
        
        stage('Test Execution') {
            steps {
                echo 'Running Unit Tests and Integration Tests...'
            }
            post {
                always {
                    emailext to: "${env.EMAIL}",
                             subject: "Test Result: Unit and Integration - ${currentBuild.currentResult}",
                             body: "The result of Unit and Integration Tests is: ${currentBuild.currentResult}. Please check the attached logs for details.",
                             attachLog: true
                }
            }
        }
        
        stage('Code Quality Check') {
            steps {
                echo 'Running code quality analysis...'
            }
        }
        
        stage('Security Check') {
            steps {
                echo 'Performing security checks...'
            }
            post {
                always {
                    emailext to: "${env.EMAIL}",
                             subject: "Security Check Result: ${currentBuild.currentResult}",
                             body: "The Security Check stage ended with: ${currentBuild.currentResult}. Logs are attached.",
                             attachLog: true
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
            }
        }
        
        stage('Staging Tests') {
            steps {
                echo 'Running checks and integration tests on the staging setup'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Starting deployment process to the production environment...'
            }
        }
    }
    
    post {
        success {
            echo 'Success!'
        }
        failure {
            echo 'Failed!'
        }
        always {
            cleanWs() 
        }
    }
}

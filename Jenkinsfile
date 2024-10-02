pipeline {
    agent any
    environment {
        // Define the necessary environment variables, such as email recipients
        EMAIL_RECIPIENTS = 'medicala.sumedh.10@gmail.com'
    }
    
    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Use Maven or another build automation tool
                sh 'mvn clean package'
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Use a test automation tool, e.g., JUnit or TestNG
                sh 'mvn test'
            }
            post {
                always {
                    // Archive test results
                    junit '**/target/surefire-reports/*.xml'
                    // Send notification email
                    script {
                        if (currentBuild.result == 'SUCCESS') {
                            emailext(
                                to: "${EMAIL_RECIPIENTS}",
                                subject: "Build Success: Unit and Integration Tests",
                                body: "The unit and integration tests passed successfully.",
                                attachLog: true
                            )
                        } else {
                            emailext(
                                to: "${EMAIL_RECIPIENTS}",
                                subject: "Build Failure: Unit and Integration Tests",
                                body: "The unit and integration tests failed. Check the attached logs for details.",
                                attachLog: true
                            )
                        }
                    }
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                echo 'Running code analysis...'
                // Use a code analysis tool like SonarQube
                sh 'sonar-scanner'
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Use a security scanning tool like OWASP Dependency Check or Snyk
                sh 'snyk test'
            }
            post {
                always {
                    // Send notification email
                    script {
                        if (currentBuild.result == 'SUCCESS') {
                            emailext(
                                to: "${EMAIL_RECIPIENTS}",
                                subject: "Build Success: Security Scan",
                                body: "The security scan passed successfully.",
                                attachLog: true
                            )
                        } else {
                            emailext(
                                to: "${EMAIL_RECIPIENTS}",
                                subject: "Build Failure: Security Scan",
                                body: "The security scan failed. Check the attached logs for details.",
                                attachLog: true
                            )
                        }
                    }
                }
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                // Simulate deployment to staging, e.g., using SSH or AWS CLI
                sh 'scp target/app.jar user@staging-server:/path/to/deploy'
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging server...'
                // Simulate integration tests on the staging server
                sh 'ssh user@staging-server "/path/to/tests.sh"'
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                // Simulate deployment to production
                sh 'scp target/app.jar user@production-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            // Cleanup actions, if necessary
            echo 'Cleaning up...'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Compilation') {
            steps {
                echo 'Compiling the project...'
                // Example for Java: sh 'mvn clean install'
                echo 'Compilation completed using Maven.'
            }
        }

        stage('Testing') {
            steps {
                echo 'Executing unit and integration tests...'
                // Example for Java: sh 'mvn test'
                echo 'Tests executed using JUnit.'
            }
        }

        stage('Static Code Analysis') {
            steps {
                echo 'Running static code analysis...'
                // Example: sh 'sonar-scanner'
                echo 'Static code analysis completed using SonarQube.'
            }
        }

        stage('Vulnerability Scan') {
            steps {
                echo 'Conducting security vulnerability scan...'
                // Example: sh 'dependency-check.sh'
                echo 'Security vulnerability scan completed using OWASP Dependency-Check.'
            }
        }

        stage('Deploy to QA') {
            steps {
                echo 'Deploying to QA environment...'
                // Example: sh 'scp target/myapp.war user@qa-server:/path/to/deploy/'
                echo 'Deployment to QA environment completed.'
            }
        }

        stage('Validation Tests on QA') {
            steps {
                echo 'Executing integration tests on QA environment...'
                // Example: sh 'mvn verify -Pqa'
                echo 'QA integration tests completed.'
            }
        }

        stage('Production Deployment') {
            steps {
                echo 'Initiating deployment to Production...'
                // Example: sh 'scp target/myapp.war user@prod-server:/path/to/deploy/'
                echo 'Deployment to Production environment completed.'
            }
        }
    }

    post {
        always {
            echo 'Triggering email notification...'
            emailext (
                subject: "Jenkins Pipeline Execution: ${currentBuild.fullDisplayName}",
                body: "Pipeline finished with result: ${currentBuild.currentResult}",
                to: 'medicala.sumedh.10@gmail.com',
                attachLog: true
            )
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example for Java: sh 'mvn clean install'
                echo 'Build completed using Maven.'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example for Java: sh 'mvn test'
                echo 'Tests completed using JUnit.'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                // Example: sh 'sonar-scanner'
                echo 'Code analysis completed using SonarQube.'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Example: sh 'dependency-check.sh'
                echo 'Security scan completed using OWASP Dependency-Check.'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Example: sh 'scp target/myapp.war user@staging-server:/path/to/deploy/'
                echo 'Deployment to Staging completed.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on Staging...'
                // Example: sh 'mvn verify -Pstaging'
                echo 'Staging integration tests completed.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Example: sh 'scp target/myapp.war user@production-server:/path/to/deploy/'
                echo 'Deployment to Production completed.'
            }
        }
    }
    

 pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Your build steps here
                echo 'Building...'
            }
        }
    }
    post {
        always {
            emailext(
                subject: "Build ${currentBuild.fullDisplayName}",
                body: "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL}) has finished",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'CulpritsRecipientProvider']],
                to: 'your-email@example.com'
            )
        }
    }
}


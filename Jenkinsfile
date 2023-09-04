pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Use Maven to build the code
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                // Run unit tests (e.g., JUnit)
                sh 'mvn test'
                
                // Run integration tests (e.g., Selenium, JUnit)
                sh 'mvn integration-test'
            }
        }

        stage('Code Analysis') {
            steps {
                // Integrate a code analysis tool (e.g., SonarQube)
                sh 'sonar-scanner'
            }
        }

        stage('Security Scan') {
            steps {
                // Perform a security scan (e.g., OWASP ZAP, Checkmarx)
                sh 'security-scan-command'
            }
        }

        stage('Deploy to Staging') {
            steps {
                // Deploy the application to a staging server (e.g., AWS EC2)
                sh 'deploy-to-staging-command'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on the staging environment
                sh 'run-staging-integration-tests-command'
            }
        }

        stage('Deploy to Production') {
            steps {
                // Deploy the application to a production server (e.g., AWS EC2)
                sh 'deploy-to-production-command'
            }
        }
    }

    post {
        success {
            // Send a success email notification with logs
            emailext (
                subject: 'Pipeline Success',
                body: 'The Jenkins pipeline completed successfully.',
                attachmentsPattern: '**/*.log', // Attach log files
                to: 'your-email@example.com'
            )
        }
        failure {
            // Send a failure email notification with logs
            emailext (
                subject: 'Pipeline Failure',
                body: 'The Jenkins pipeline failed. Please investigate.',
                attachmentsPattern: '**/*.log', // Attach log files
                to: 'your-email@example.com'
            )
        }
    }
}

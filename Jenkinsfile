pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven.'
                // Example command to generate a build log
                sh 'echo "Build log" > build.log'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit...'
                echo 'Running integration tests with Selenium...'
                // Example commands to generate test logs
                sh 'echo "Unit test log" > unit-test.log'
                sh 'echo "Integration test log" > integration-test.log'
            }
            post {
                always {
                    // Archive test results or other logs (if available)
                    archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
                    
                    // Send email with the logs attached
                    emailext (
                        to: "yashpansuria80@gmail.com",
                        subject: "Test Stage - Build #${currentBuild.number}",
                        body: "The Unit and Integration Tests stage has completed. Please find the logs attached.",
                        attachments: '**/*.log' // Use the correct parameter for attachments
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality with SonarQube...'
                // Example command to generate code analysis log
                sh 'echo "Code analysis log" > code-analysis.log'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities with SAST scanner...'
                // Example command to generate security scan log
                sh 'echo "Security scan log" > security-scan.log'
            }
            post {
                always {
                    // Send email with the logs attached
                    emailext (
                        to: "yashpansuria80@gmail.com",
                        subject: "Security Scan Stage - Build #${currentBuild.number}",
                        body: "The Security Scan stage has completed. Please find the logs attached.",
                        attachments: '**/*.log' // Use the correct parameter for attachments
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to staging server using AWS...'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to production server using AWS tools...'
            }
        }
    }

    post {
        success {
            emailext (
                to: "yashpansuria80@gmail.com",
                subject: "Pipeline Success - Build #${currentBuild.number}",
                body: "The pipeline has successfully completed all stages. Congratulations!",
                attachments: '**/*.log' // Use the correct parameter for attachments
            )
        }
        failure {
            emailext (
                to: "yashpansuria80@gmail.com",
                subject: "Pipeline Failure - Build #${currentBuild.number}",
                body: "The pipeline has failed. Please review the logs for more details.",
                attachments: '**/*.log' // Use the correct parameter for attachments
            )
        }
    }
}

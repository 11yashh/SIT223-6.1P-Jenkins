pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit...'
                echo 'Running integration tests with Selenium...'
            }
            post {
                always {
                    // Archive logs or test results
                    archiveArtifacts artifacts: '**/test-results/*.xml', allowEmptyArchive: true

                    // Send email with a link to the Jenkins build page and log information
                    mail to: "yashpansuria80@gmail.com",
                        subject: "Test Stage Completion - Build #${currentBuild.number}",
                        body: """
                        The Unit and Integration Tests stage has completed.

                        Build Number: ${currentBuild.number}
                        Build URL: ${env.BUILD_URL}

                        Please check the full console output and artifacts here: ${env.BUILD_URL}/console
                        Logs and test results can be downloaded as artifacts.
                        """
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality with SonarQube...'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities with SAST scanner...'
            }
            post {
                always {
                    // Archive logs for security scan if available
                    archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true

                    // Send email with a link to the Jenkins build page and log information
                    mail to: "yashpansuria80@gmail.com",
                        subject: "Security Scan Completion - Build #${currentBuild.number}",
                        body: """
                        The Security Scan stage has completed.

                        Build Number: ${currentBuild.number}
                        Build URL: ${env.BUILD_URL}

                        Please check the full console output and artifacts here: ${env.BUILD_URL}/console
                        Logs can be downloaded as artifacts.
                        """
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
            mail to: "yashpansuria80@gmail.com",
                subject: "Pipeline Success - Build #${currentBuild.number}",
                body: """
                The pipeline has successfully completed all stages.

                Build Number: ${currentBuild.number}
                Build URL: ${env.BUILD_URL}

                Please check the full console output and artifacts here: ${env.BUILD_URL}/console
                Logs can be downloaded as artifacts.
                """
        }
        failure {
            mail to: "yashpansuria80@gmail.com",
                subject: "Pipeline Failure - Build #${currentBuild.number}",
                body: """
                The pipeline has failed.

                Build Number: ${currentBuild.number}
                Build URL: ${env.BUILD_URL}

                Please check the full console output and artifacts here: ${env.BUILD_URL}/console
                Logs can be downloaded as artifacts.
                """
        }
    }
}

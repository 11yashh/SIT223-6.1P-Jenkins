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
                    // Send email with link to Jenkins logs (console output)
                    mail to: "yashpansuria80@gmail.com",
                        subject: "Test Stage Completion - Build #${currentBuild.number}",
                        body: """
                        The Unit and Integration Tests stage has completed.

                        You can view the logs here: ${env.BUILD_URL}console
                        """
                    attachments: [
                          (fileName: 'console.txt', content: '${readFile('console')})  // Replace colon with closing parenthesis
                    ],
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
                    // Send email with link to Jenkins logs (console output)
                    mail to: "yashpansuria80@gmail.com",
                        subject: "Security Scan Completion - Build #${currentBuild.number}",
                        body: """
                        The Security Scan stage has completed.

                        You can view the logs here: ${env.BUILD_URL}console
                        """
                    attachments: [
                          (fileName: 'console.txt', content: '${readFile('console')})  // Replace colon with closing parenthesis
                    ],
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

                You can view the logs here: ${env.BUILD_URL}console
                """
            attachments: [
                          (fileName: 'console.txt', content: '${readFile('console')})  // Replace colon with closing parenthesis
                    ],
            
        }
        failure {
            mail to: "yashpansuria80@gmail.com",
                subject: "Pipeline Failure - Build #${currentBuild.number}",
                body: """
                The pipeline has failed.

                You can view the logs here: ${env.BUILD_URL}console
                """
            attachments: [
                          (fileName: 'console.txt', content: '${readFile('console')})  // Replace colon with closing parenthesis
                    ],
            
        }
    }
}

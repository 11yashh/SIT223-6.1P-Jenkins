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
                   

                    // Send email with a link to the Jenkins build page and log information
                    mail to: "yashpansuria80@gmail.com",
                        subject: "Security Scan Completion - Build #${currentBuild.number}",
                        body: """
                        Logs: Scanning for vulnerabilities with SAST scanner...
                        The Security Scan stage has completed.

                       Build URL: ${env.BUILD_URL} """
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
                Logs: Completed Scan
                The pipeline has successfully completed all stages.

                 Build URL: ${env.BUILD_URL} """
        }
        failure {
            mail to: "yashpansuria80@gmail.com",
                subject: "Pipeline Failure - Build #${currentBuild.number}",
                body: """
                Logs: Failed Scan
                The pipeline has failed.

                Build URL: ${env.BUILD_URL}"""

                
        }
    }
}

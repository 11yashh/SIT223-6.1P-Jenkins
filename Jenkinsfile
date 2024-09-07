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
                    // Archive test results or other logs (if available)
                    archiveArtifacts artifacts: '**/test-results/*.xml', allowEmptyArchive: true
                    
                    // Send email with the logs attached
                    
                       mail to: "yashpansuria80@gmail.com",
                        subject: "Test Stage - Build #${currentBuild.number}",
                        body: "The Unit and Integration Tests stage has completed. Please find the logs attached.",
                        attachmentsPattern: '**/log/**/*.log'
                    
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
                    // Send email with the logs attached
                   
                       mail to: "yashpansuria80@gmail.com",
                        subject: "Security Scan Stage - Build #${currentBuild.number}",
                        body: "The Security Scan stage has completed. Please find the logs attached.",
                        attachmentsPattern: '**/log/**/*.log'
                    
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
                body: "The pipeline has successfully completed all stages. Congratulations!"
                attachmentsPattern: '**/log/**/*.log'
            
        }
        failure {
            
                mail to: "yashpansuria80@gmail.com",
                subject: "Pipeline Failure - Build #${currentBuild.number}",
                body: "The pipeline has failed. Please review the logs for more details.",
                attachmentsPattern: '**/log/**/*.log'
            
        }
    }
}

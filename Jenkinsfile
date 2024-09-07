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
                // Save the log to a file
                script {
                    writeFile file: 'unit_test_log.txt', text: currentBuild.rawBuild.getLog().join("\n")
                }
            } 
            post {
                always {
                    // Archive the log file
                    archiveArtifacts artifacts: 'unit_test_log.txt', allowEmptyArchive: true
                    // Send an email with the log attached
                    emailext to: "yashpansuria80@gmail.com", 
                        subject: "Test Stage Completion - Build # ${currentBuild.number}", 
                        body: "The Unit and Integration Tests stage has completed. Logs are attached.",
                        attachmentsPattern: 'unit_test_log.txt'
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
                // Save the log to a file
                script {
                    writeFile file: 'security_scan_log.txt', text: currentBuild.rawBuild.getLog().join("\n")
                }
            } 
            post {
                always {
                    // Archive the log file
                    archiveArtifacts artifacts: 'security_scan_log.txt', allowEmptyArchive: true
                    // Send an email with the log attached
                    emailext to: "yashpansuria80@gmail.com", 
                        subject: "Security Scan Completion - Build # ${currentBuild.number}", 
                        body: "The Security Scan stage has completed. Logs are attached.",
                        attachmentsPattern: 'security_scan_log.txt'
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
            subject: "Pipeline Success - Build # ${currentBuild.number}", 
            body: "The pipeline has successfully completed all stages. Build logs are attached." 
        } 
        failure { 
            mail to: "yashpansuria80@gmail.com", 
            subject: "Pipeline Failure - Build # ${currentBuild.number}", 
            body: "The pipeline has failed. Build logs are attached." 
        } 
    } 
}

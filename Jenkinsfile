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
                success { 
                    script {
                        def logFile = "${env.WORKSPACE}/unit_integration_tests_log.txt"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')
                        mail to: "yashpansuria80@gmail.com", 
                             subject: "Unit & Integration Tests Success - Build # ${currentBuild.number}", 
                             body: "The Unit & Integration Tests stage has completed successfully. Build logs are attached.", 
                             attachmentsPattern: 'unit_integration_tests_log.txt'
                    }
                } 
                failure { 
                    script {
                        def logFile = "${env.WORKSPACE}/unit_integration_tests_log.txt"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')
                        mail to: "yashpansuria80@gmail.com", 
                             subject: "Unit & Integration Tests Failure - Build # ${currentBuild.number}", 
                             body: "The Unit & Integration Tests stage has failed. Build logs are attached.", 
                             attachmentsPattern: 'unit_integration_tests_log.txt'
                    }
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
                success { 
                    script {
                        def logFile = "${env.WORKSPACE}/security_scan_log.txt"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')
                        mail to: "yashpansuria80@gmail.com", 
                             subject: "Security Scan Success - Build # ${currentBuild.number}", 
                             body: "The Security Scan stage has completed successfully. Build logs are attached.", 
                             attachmentsPattern: 'security_scan_log.txt'
                    }
                } 
                failure { 
                    script {
                        def logFile = "${env.WORKSPACE}/security_scan_log.txt"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')
                        mail to: "yashpansuria80@gmail.com", 
                             subject: "Security Scan Failure - Build # ${currentBuild.number}", 
                             body: "The Security Scan stage has failed. Build logs are attached.", 
                             attachmentsPattern: 'security_scan_log.txt'
                    }
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
            script {
                def logFile = "${env.WORKSPACE}/pipeline_log.txt"
                writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')
                mail to: "yashpansuria80@gmail.com", 
                     subject: "Pipeline Success - Build # ${currentBuild.number}", 
                     body: "The pipeline has successfully completed all stages. Build logs are attached.", 
                     attachmentsPattern: 'pipeline_log.txt'
            }
        } 
        failure { 
            script {
                def logFile = "${env.WORKSPACE}/pipeline_log.txt"
                writeFile file: logFile, text: currentBuild.rawBuild.getLog().join('\n')
                mail to: "yashpansuria80@gmail.com", 
                     subject: "Pipeline Failure - Build # ${currentBuild.number}", 
                     body: "The pipeline has failed. Build logs are attached.", 
                     attachmentsPattern: 'pipeline_log.txt'
            }
        } 
    } 
}


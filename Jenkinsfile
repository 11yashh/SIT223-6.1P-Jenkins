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
                        def logs = currentBuild.rawBuild.getLog(100).join("\n")
                        mail to: "yashpansuria80@gmail.com",
                        subject: "Unit & Integration Tests Success - Build # ${currentBuild.number}",
                        body: "The Unit & Integration Tests stage has completed successfully.\n\nLogs:\n${logs}"
                    }
                }
                failure {
                    script {
                        def logs = currentBuild.rawBuild.getLog(100).join("\n")
                        mail to: "yashpansuria80@gmail.com",
                        subject: "Unit & Integration Tests Failure - Build # ${currentBuild.number}",
                        body: "The Unit & Integration Tests stage has failed.\n\nLogs:\n${logs}"
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
                        def logs = currentBuild.rawBuild.getLog(100).join("\n")
                        mail to: "yashpansuria80@gmail.com",
                        subject: "Security Scan Success - Build # ${currentBuild.number}",
                        body: "The Security Scan stage has completed successfully.\n\nLogs:\n${logs}"
                    }
                }
                failure {
                    script {
                        def logs = currentBuild.rawBuild.getLog(100).join("\n")
                        mail to: "yashpansuria80@gmail.com",
                        subject: "Security Scan Failure - Build # ${currentBuild.number}",
                        body: "The Security Scan stage has failed.\n\nLogs:\n${logs}"
                    }
                }
            }
        }
    }

    post {
        success {
            script {
                def logs = currentBuild.rawBuild.getLog(100).join("\n")
                mail to: "yashpansuria80@gmail.com",
                subject: "Pipeline Success - Build # ${currentBuild.number}",
                body: "The pipeline has successfully completed all stages.\n\nLogs:\n${logs}"
            }
        }
        failure {
            script {
                def logs = currentBuild.rawBuild.getLog(100).join("\n")
                mail to: "yashpansuria80@gmail.com",
                subject: "Pipeline Failure - Build # ${currentBuild.number}",
                body: "The pipeline has failed.\n\nLogs:\n${logs}"
            }
        }
    }
}

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
        echo 'Running unit   
 tests with JUnit...'
        echo 'Running integration tests with Selenium...'
      }
      post {
        success {
          mail to: "yashpansuria80@gmail.com",
            subject: "Unit & Integration Tests Success - Build # ${currentBuild.number}",
            body: "The Unit & Integration Tests stage has completed successfully. Build logs are attached.",
            attachments {
              // Attach build logs automatically
              primaryWorkspaceDirectories()
            }
        }
        failure {
          mail to: "yashpansuria80@gmail.com",
            subject: "Unit & Integration Tests Failure - Build # ${currentBuild.number}",
            body: "The Unit & Integration Tests stage has failed. Build logs are attached.",
            attachments {
              // Attach build logs automatically
              primaryWorkspaceDirectories()
            }
        }
      }
    }
    stage('Code Analysis') {
      steps {
        echo 'Analyzing code quality with SonarQube...'
      }
      post {
        success {
          mail to: "yashpansuria80@gmail.com",
            subject: "Code Analysis Success - Build # ${currentBuild.number}",
            body: "The Code Analysis stage has completed successfully. Build logs are attached.",
            attachments {
              // Attach build logs automatically
              primaryWorkspaceDirectories()
            }
        }
        failure {
          mail to: "yashpansuria80@gmail.com",
            subject: "Code Analysis Failure - Build # ${currentBuild.number}",
            body: "The Code Analysis stage has failed. Build logs are attached.",
            attachments {
              // Attach build logs automatically
              primaryWorkspaceDirectories()
            }
        }
      }
    }
    stage('Security Scan') {
      steps {
        echo 'Scanning for vulnerabilities with SAST scanner...'
      }
      post {
        success {
          mail to: "yashpansuria80@gmail.com",
            subject: "Security Scan Success - Build # ${currentBuild.number}",
            body: "The Security Scan stage has completed successfully. Build logs are attached.",
            attachments {
              // Attach build logs automatically
              primaryWorkspaceDirectories()
            }
        }
        failure {
          mail to: "yashpansuria80@gmail.com",
            subject: "Security Scan Failure - Build # ${currentBuild.number}",
            body: "The Security Scan stage has failed. Build logs are attached.",
            attachments {
              // Attach build logs automatically
              primaryWorkspaceDirectories()
            }
        }
      }
    }
    // ... other stages ...
  }

  post {
    success {
      mail to: "yashpansuria80@gmail.com",
        subject: "Pipeline Success - Build # ${currentBuild.number}",
        body: "The pipeline has successfully completed all stages. Build logs are attached.",
        attachments {
          // Attach build logs automatically
          primaryWorkspaceDirectories()
        }
    }
    failure {
      mail to: "yashpansuria80@gmail.com",
        subject: "Pipeline Failure - Build # ${currentBuild.number}",
        body: "The pipeline has failed. Build logs are attached.",
        attachments {
          // Attach build logs automatically
          primaryWorkspaceDirectories()
        }
    }
  }
}

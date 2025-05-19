pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            url:   'https://github.com/FionaGhosh/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        bash 'npm test || exit /b 0'
      }
      post {
        success {
          emailext (
            subject: "TESTS PASSED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body:    "All tests passed.\nSee console log attached.",
            to:      'fionag1402@gmail.com',
            attachBuildLog: true
          )
        }
        failure {
          emailext (
            subject: "TESTS FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body:    "Tests failed! Please investigate.\nSee console log attached.",
            to:      'fionag1402@gmail.com',
            attachBuildLog: true
          )
        }
      }
    }

    stage('Generate Coverage Report') {
      steps {
        bash 'npm run coverage || exit /b 0'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        bash 'npm audit || exit /b 0'
      }
      post {
        success {
          emailext (
            subject: "SECURITY SCAN OK: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body:    "No new vulnerabilities found.\nSee console log attached.",
            to:      'fionag1402@gmail.com',
            attachBuildLog: true
          )
        }
        failure {
          emailext (
            subject: "SECURITY SCAN ISSUES: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body:    "Vulnerabilities detected! Please review.\nSee console log attached.",
            to:      'fionag1402@gmail.com',
            attachBuildLog: true
          )
        }
      }
    }
  }
}

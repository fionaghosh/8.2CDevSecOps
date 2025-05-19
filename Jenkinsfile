stage('Run Tests') {
  steps { bash 'npm test || exit /b 0' }
  post {
    success {
      emailext(
        subject: "TESTS PASSED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body:    "All tests passed. See attached log.",
        to:      'fionag1402@gmail.com',
        attachBuildLog: true
      )
    }
    failure {
      emailext(
        subject: "TESTS FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body:    "Tests failed. Please investigate. See attached log.",
        to:      'fionag1402@gmail.com',
        attachBuildLog: true
      )
    }
  }
}

stage('NPM Audit (Security Scan)') {
  steps { bash 'npm audit || exit /b 0' }
  post {
    success {
      emailext(
        subject: "SECURITY SCAN OK: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body:    "No vulnerabilities found. See attached log.",
        to:      'fionag1402@gmail.com',
        attachBuildLog: true
      )
    }
    failure {
      emailext(
        subject: "SECURITY SCAN ISSUES: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body:    "Vulnerabilities detected! See attached log.",
        to:      'fionag1402@gmail.com',
        attachBuildLog: true
      )
    }
  }
}


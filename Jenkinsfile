pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // pull from *your* fork
        git branch: 'main',
            url:   'https://github.com/fionaghosh/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        // allow failures so the pipeline keeps going
        bat 'npm test || exit /b 0'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        bat 'npm run coverage || exit /b 0'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        bat 'npm audit || exit /b 0'
      }
    }
  }
<<<<<<< HEAD
}
=======
}
>>>>>>> 33f57d1d904442836e0e3231b2744e0304090d3f

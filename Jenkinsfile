pipeline {
  agent {
      docker {
          image 'node:lts-buster-slim'
          args '-p 3000:3000'
      }
  }
  environment {
    CI = 'true'
  }

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  stages {
    stage('Install dependencies') {
      steps {
        sh 'npm i'
      }
    }
    stage('Run tests') {
      steps {
        sh 'npm test'
      }
    }
  }
}
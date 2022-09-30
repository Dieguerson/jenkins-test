pipeline {
  agent any
  tools {
    nodejs 'node-11.0.0'
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
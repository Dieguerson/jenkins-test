pipeline {
  agent any
  tools {
    nodejs 'node'
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
  post{
    success {
      setBuildStatus("Build succeeded", "SUCCESS");
    }
    failure {
      setBuildStatus("Build failed", "FAILURE");
    } 
  }
}

void setBuildStatus(String message, String state) {
    step([
        $class: "GitHubCommitStatusSetter",
        reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/matiasmancilla/jenkins-test"],
        contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
        errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
        statusResultSource: [$class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]]]
    ]);
}

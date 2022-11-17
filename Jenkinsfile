pipeline {
  agent any
  stages {
    stage('verify version') {
      steps {
        sh 'php --version'
      }
    }
    stage('Integration') {
      steps {
        sh 'php 3203website.php'
      }
    }
  }
}

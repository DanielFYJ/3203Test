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
    stage('OWASP DependencyCheck') {
      steps {
	dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
      }
     }
}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
  }
}

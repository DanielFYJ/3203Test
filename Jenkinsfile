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
    stage('SonarQube Analysis'){
      steps {	 
	script {
		def scannerHome = tool 'SonarQube';
		withSonarQubeEnv('SonarQube') {
		sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=3203PHP -Dsonar.sources=."
				}
			}
		}
	}
}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
		always {
			recordIssues enabledForFailure: true, tool: sonarQube()
		}
	}
  }


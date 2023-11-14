pipeline {
	agent any
	stages {
		stage ('Checkout') {
			steps {
				git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
			}
		}
		stage('Code Quality Check via SonarQube') {
			steps {
				script {
					def scannerHome = tool 'SonarQube';
					withSonarQubeEnv('SonarQube') {
					sh "${scannerHome}/bin/sonar-scanner -X -Dsonar.projectKey=OWASP - Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqp_744b589e9d36238f544e1a165d2d71689aa0e9e6"
					}
				}
			}
		}
	}
	post {
		always {
			recordIssues enabledForFailure: true, tool: sonarQube()
		}
	}
}

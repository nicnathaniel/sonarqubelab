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
					def scannerHome = tool 'SonarQube'
					withSonarQubeEnv('SonarQube') {
						sh "${scannerHome}/bin/sonar-scanner -X -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.token=sqp_6ad84717abdc1221ff2978c9b270153bd2291f3a"
					}
				}
			}
		}
	}
	post {
		always {
			recordIssues enabledForFailure: true, tool: [sonarQube()]
		}
	}
}

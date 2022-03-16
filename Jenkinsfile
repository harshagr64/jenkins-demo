pipeline {
  agent any
  stages {
		stage('SonarQube Code Analyzer') {
		environment {
			scannerHome = tool 'Sonar Scanner'
		}
		steps {
			withSonarQubeEnv('SonarQube') {
				sh "${tool("Sonar Scanner")}/bin/sonar-scanner \
			 -Dsonar.projectKey=task2-jenkins \
			 -Dsonar.sources=. \
			 -Dsonar.host.url=http://localhost:9000 \
			 -Dsonar.login=6da68ec34f6218ec363cad360646b9e601d51c09"
			}
			timeout(time: 10, unit: 'MINUTES') {
					waitForQualityGate abortPipeline: true
			}
      sh 'git push origin release/uat'
		}
    }
  }
}

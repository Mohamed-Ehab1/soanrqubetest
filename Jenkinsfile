node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'suiiz';
    withSonarQubeEnv() {
      sh "chmod +x sonar-scanner && sonar-scanner -Dsonar.projectKey=pytest -Dsonar.sources=."
    }
  }
}


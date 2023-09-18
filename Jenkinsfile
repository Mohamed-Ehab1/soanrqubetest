node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'suiiz';
    withSonarQubeEnv() {
      sh "sonar-scanner ./"
    }
  }
}


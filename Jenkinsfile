node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'suiiz';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner --version"
    }
  }
}
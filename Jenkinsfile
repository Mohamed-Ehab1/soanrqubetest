node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'suiiz';
    withSonarQubeEnv() {
      sh "echo hello"
    }
  }
}


node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'suiiz'
    withSonarQubeEnv() {
      sh '''
        sonar-scanner \
        -Dsonar.projectKey=pytest \
        -Dsonar.sources=. \
        -Dsonar.host.url=https://sonarqube.suiiz.net \
        -Dsonar.token=sqp_72743c4c6d6d279e29ead1284261351b2c2dfc10
      '''
    }
  }
}

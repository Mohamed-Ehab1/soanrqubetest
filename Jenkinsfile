node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'suiiz'
    withSonarQubeEnv() {
      sh '''
        echo "deb http://deb.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list && \
        apt-get update && \
        apt-get install -y -t jessie-backports openjdk-8-jre-headless ca-certificates-java && \
        sonar-scanner
      '''
    }
  }
}

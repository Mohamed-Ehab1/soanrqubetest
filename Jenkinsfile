pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Python code repository
                checkout scm
            }
        }
        stage('SonarQube Scan') {
            steps {
                script {
                    def scannerHome = tool name: 'suiiz', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    withEnv(["PATH+SONARSCANNER=${scannerHome}/bin"]) {
                        sh """
                        sonar-scanner \
                            -Dsonar.projectKey=pytest \
                            -Dsonar.sources=.
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'SonarQube analysis passed. You can check the results on SonarQube server.'
        }
        failure {
            echo 'SonarQube analysis failed. Check the SonarQube dashboard for issues.'
        }
    }
}

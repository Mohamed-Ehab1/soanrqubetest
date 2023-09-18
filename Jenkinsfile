pipeline {
    agent any

    tools {
        // Define the SonarQube Scanner tool installation name
        // Use the name you provided in the Global Tool Configuration
        tool 'suiiz'
    }

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
                    def scannerHome = tool 'suiiz'
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

pipeline {
    stages {
        stage('Checkout') {
            steps {
                // Checkout your Python code repository
                checkout scm
            }
        }
        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('suiiz') {
                    sh """
                    #!/bin/bash
                    sonar-scanner \
                        -Dsonar.projectKey=pytest \
                        -Dsonar.sources=.
                    """
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

pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Clone the SimpleTest repository
                checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/Mohamed-Ehab1/soanrqubetest']]])
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Composer dependencies
                sh 'composer install'
            }
        }

        stage('Unit Tests') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    sh 'php artisan test'
                }
                script {
                    // Update the GitHub pull request status
                    currentBuild.result = currentBuild.resultIsBetterOrEqualTo('SUCCESS') ? 'SUCCESS' : 'FAILURE'
                    def github = getGitHub()
                    def pr = github.getPullRequest(env.CHANGE_ID)
                    pr.createReview('Automated Jenkins Build', currentBuild.result, 'Automated Jenkins build result')
                }
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/phpunit.result.cache', allowEmptyArchive: true
            }
        }
    }
    
    post {
        success {
            // Notify GitHub of a successful build
            script {
                currentBuild.result = 'SUCCESS'
                def github = getGitHub()
                def pr = github.getPullRequest(env.CHANGE_ID)
                pr.createReview('Jenkins Build', 'APPROVE', 'Jenkins build passed successfully.')
            }
        }
        failure {
            // Notify GitHub of a failed build
            script {
                currentBuild.result = 'FAILURE'
                def github = getGitHub()
                def pr = github.getPullRequest(env.CHANGE_ID)
                pr.createReview('Jenkins Build', 'REQUEST_CHANGES', "Jenkins build failed. Please fix the issues. Result: ${currentBuild.result}")
            }
        }
    }
}

pipeline {
    agent any

    tools {
        nodejs 'NodeJS-20'
    }

    stages {

        stage('Environment Check') {
            steps {
                sh 'node --version'
                sh 'npm --version'
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm ci'
                    sh 'npm run build'
                }
            }
        }

        stage('Build Backend') {
            steps {
                dir('backend') {
                    sh 'npm ci'
                }
            }
        }
    }

    post {
        success {
            echo 'NurtiFlow CI pipeline completed successfully!'
        }

        failure {
            echo 'NurtiFlow CI pipeline failed. Check the Jenkins console output.'
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}

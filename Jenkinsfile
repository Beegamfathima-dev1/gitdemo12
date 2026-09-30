pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Build Backend') {
            steps {
                dir('backend') {
                    bat 'npm install'
                }
            }
        }

        stage('Test') {
            parallel {

                stage('Frontend Tests') {
                    steps {
                        dir('frontend') {
                            bat 'npm test -- --watchAll=false'
                        }
                    }
                }

                stage('Backend Tests') {
                    steps {
                        dir('backend') {
                            bat 'npm test'
                        }
                    }
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

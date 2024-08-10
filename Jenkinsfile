pipeline {
    agent any

    stages {
        stage('Backend Build') {
            agent {
                docker {
                    image 'node:16-alpine'
                    args '-v /var/lib/jenkins/workspace:/workspace'
                }
            }
            steps {
                script {
                    dir('backend') {
                        sh 'npm install'
                        sh 'npm run build'
                    }
                }
            }
        }

        stage('Frontend Build') {
            agent {
                docker {
                    image 'node:16-alpine'
                    args '-v /var/lib/jenkins/workspace:/workspace'
                }
            }
            steps {
                script {
                    dir('frontend') {
                        sh 'npm install'
                        sh 'npm run build'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

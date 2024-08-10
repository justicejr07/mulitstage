pipeline {
    agent any


    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git url: 'https://github.com/justicejr07/mulitstage.git', branch: 'main'
            }
        }

        stage('Backend Build') {
            agent {
                docker {
                    image 'maven:3.8.1-adoptopenjdk-11'
                    args '-v /var/lib/jenkins/workspace:/workspace'
                }
            }
            steps {
                dir('backend') {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Backend Test') {
            agent {
                docker {
                    image 'maven:3.8.1-adoptopenjdk-11'
                    args '-v /var/lib/jenkins/workspace:/workspace'
                }
            }
            steps {
                dir('backend') {
                    sh 'mvn test'
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
                dir('frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Frontend Test') {
            agent {
                docker {
                    image 'node:16-alpine'
                    args '-v /var/lib/jenkins/workspace:/workspace'
                }
            }
            steps {
                dir('frontend') {
                    sh 'npm run test'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy steps, e.g., upload to S3, deploy to Kubernetes, etc.
                echo 'Deploying the application...'
                // Example: sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }

    post {
        always {
            // Cleanup or notifications
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

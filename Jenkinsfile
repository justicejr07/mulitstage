pipeline {
    agent none
    stages {
        stage('Back-end') {
            agent {
                docker { image 'openjdk:11-jdk-slim' }
            }
            steps {
                sh 'java -version'
            }
        }
        stage('Front-end') {
            agent {
                docker { image 'node:16-alpine' }
            }
            steps {
                sh 'node --version'
            }
        }
    }
}


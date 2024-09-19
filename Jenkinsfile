pipeline {
    agent any

    stages {
        stage('Build Frontend Docker Image') {
            steps {
                sh 'docker build -t frontend:latest  -f api/Dockerfile'
            }
        }

        stage('Run Frontend Docker Container') {
            steps {
                sh 'docker run -d frontend:latest'
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                sh 'docker build -t backend:latest  -f client/Dockerfile'
            }
        }

        stage('Run Backend Docker Container') {
            steps {
                sh 'docker run -d backend:latest'
            }
        }
    }

    post {
        always {
            script {
                sh 'docker rmi -f frontend:latest || echo "Image frontend:latest not found"'
                sh 'docker rmi -f backend:latest || echo "Image backend:latest not found"'
            }
        }
    }
}





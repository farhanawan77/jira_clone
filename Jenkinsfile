pipeline {
    agent any

    stages {
        stage('Build Frontend Docker Image') {
            steps {
                script {
                    echo 'Building Frontend Docker Image...'
                    sh 'docker build -t frontend:latest -f api/Dockerfile api/'
                }
            }
        }

        stage('Run Frontend Docker Container') {
            steps {
                script {
                    echo 'Running Frontend Docker Container...'
                    sh 'docker run -d --name frontend frontend:latest'
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                script {
                    echo 'Building Backend Docker Image...'
                    sh 'docker build -t backend:latest -f client/Dockerfile client/'
                }
            }
        }

        stage('Run Backend Docker Container') {
            steps {
                script {
                    echo 'Running Backend Docker Container...'
                    sh 'docker run -d --name backend backend:latest'
                }
            }
        }
    }

    post {
        always {
            script {
                echo 'Cleaning up Docker images and containers...'
                sh 'docker stop frontend || echo "Container frontend not found"'
                sh 'docker rm frontend || echo "Container frontend not found"'
                sh 'docker stop backend || echo "Container backend not found"'
                sh 'docker rm backend || echo "Container backend not found"'
                sh 'docker rmi -f frontend:latest || echo "Image frontend:latest not found"'
                sh 'docker rmi -f backend:latest || echo "Image backend:latest not found"'
            }
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Build Frontend Docker Image') {
            steps {
                script {
                    try {
                        sh 'docker build -t frontend:latest -f api/Dockerfile api/'
                    } catch (Exception e) {
                        echo "Failed to build frontend: ${e.message}"
                    }
                }
            }
        }

        stage('Run Frontend Docker Container') {
            steps {
                script {
                    try {
                        sh 'docker run -d frontend:latest'
                    } catch (Exception e) {
                        echo "Failed to run frontend: ${e.message}"
                    }
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                script {
                    try {
                        sh 'docker build -t backend:latest -f client/Dockerfile client/'
                    } catch (Exception e) {
                        echo "Failed to build backend: ${e.message}"
                    }
                }
            }
        }

        stage('Run Backend Docker Container') {
            steps {
                script {
                    try {
                        sh 'docker run -d backend:latest'
                    } catch (Exception e) {
                        echo "Failed to run backend: ${e.message}"
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                try {
                    sh 'docker rmi -f frontend:latest'
                } catch (Exception e) {
                    echo "Image frontend:latest not found: ${e.message}"
                }
                try {
                    sh 'docker rmi -f backend:latest'
                } catch (Exception e) {
                    echo "Image backend:latest not found: ${e.message}"
                }
            }
        }
    }
}




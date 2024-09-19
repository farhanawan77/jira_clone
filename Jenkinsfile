pipeline {
    agent any

    stages {
        stage('Build Frontend Docker Image') {
            steps {
                script {
                    echo "Building Frontend Docker Image"
                    def buildResult = sh(script: 'docker build -t frontend:latest -f api/Dockerfile api/', returnStatus: true)
                    if (buildResult != 0) {
                        error("Frontend build failed with status ${buildResult}. Check the Dockerfile and build context.")
                    }
                }
            }
        }

        stage('Run Frontend Docker Container') {
            steps {
                script {
                    echo "Running Frontend Docker Container"
                    def runResult = sh(script: 'docker run -d --name frontend_container frontend:latest', returnStatus: true)
                    if (runResult != 0) {
                        error("Failed to run frontend container with status ${runResult}")
                    }
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                script {
                    echo "Building Backend Docker Image"
                    def buildResult = sh(script: 'docker build -t backend:latest -f client/Dockerfile client/', returnStatus: true)
                    if (buildResult != 0) {
                        error("Backend build failed with status ${buildResult}. Check the Dockerfile and build context.")
                    }
                }
            }
        }

        stage('Run Backend Docker Container') {
            steps {
                script {
                    echo "Running Backend Docker Container"
                    def runResult = sh(script: 'docker run -d --name backend_container backend:latest', returnStatus: true)
                    if (runResult != 0) {
                        error("Failed to run backend container with status ${runResult}")
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                echo "Cleaning up Docker images and containers"
                sh 'docker stop frontend_container || echo "Container frontend_container not found"'
                sh 'docker rm frontend_container || echo "Container frontend_container not found"'
                sh 'docker stop backend_container || echo "Container backend_container not found"'
                sh 'docker rm backend_container || echo "Container backend_container not found"'
                sh 'docker rmi -f frontend:latest || echo "Image frontend:latest not found"'
                sh 'docker rmi -f backend:latest || echo "Image backend:latest not found"'
            }
        }
    }
}




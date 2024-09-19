pipeline {
    agent any

    stages {
        stage('Build Frontend Docker Image') {
            steps {
                script {
                    // Build the Docker image for frontend located in the 'api' folder
                    docker.build('frontend:latest', 'api/')
                }
            }
        }

        stage('Run Frontend Docker Container') {
            steps {
                script {
                    // Run the Docker container for frontend
                    docker.image('frontend:latest').run('-d -p 8080:80')
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                script {
                    // Build the Docker image for backend located in the 'client' folder
                    docker.build('backend:latest', 'client/')
                }
            }
        }

        stage('Run Backend Docker Container') {
            steps {
                script {
                    // Run the Docker container for backend
                    docker.image('backend:latest').run('-d -p 5000:5000')
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images
            script {
                sh 'docker rmi -f frontend:latest || true'
                sh 'docker rmi -f backend:latest || true'
            }
        }
    }
}



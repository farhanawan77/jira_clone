pipeline {
    agent any

    stages {
   

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image named frontend
                    docker.build('frontend:latest')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container from the frontend image
                    docker.image('frontend:latest').run('-d -p 8080:80')
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images and containers
            script {
                sh 'docker rmi -f frontend:latest || true'
            }
        }
    }
}


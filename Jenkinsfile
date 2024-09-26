pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = '......' // ID of your Docker Hub credentials
        IMAGE_NAME = 'joshnak4/image-1' // Replace with your Docker Hub username and desired image name
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from your repository
                git branch: 'main', url: 'https://github.com/Joshna454/jenkins-docker-pipeline.git' // Your GitHub repo
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Login to Docker Hub
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        // Push the Docker image
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Image pushed successfully!'
        }
        failure {
            echo 'Image push failed.'
        }
    }
}

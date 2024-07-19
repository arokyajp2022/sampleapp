pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'  // Replace with your Docker Hub credentials ID
        DOCKER_IMAGE_NAME = 'arokyajp@gmail.com/my-python-app'
        DOCKER_TAG = 'latest'  // You can use build number or commit hash as the tag
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    docker.build("${env.DOCKER_IMAGE_NAME}:${env.DOCKER_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Login to Docker Hub
                    docker.withRegistry('https://index.docker.io/v1/', "${env.DOCKER_CREDENTIALS_ID}") {
                        // Push Docker image
                        docker.image("${env.DOCKER_IMAGE_NAME}:${env.DOCKER_TAG}").push("${env.DOCKER_TAG}")
                    }
                }
            }
        }
    }
}

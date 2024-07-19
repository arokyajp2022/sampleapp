pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'  // Docker Hub credentials
        GITHUB_CREDENTIALS_ID = 'github-pat'  // GitHub PAT credentials
        DOCKER_IMAGE_NAME = 'arokyajp2022/sampleapp'  // Correct format
        DOCKER_TAG = 'latest'  // You can use build number or commit hash as the tag
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: 'https://github.com/arokyajp2022/sampleapp.git',
                                               credentialsId: "${env.GITHUB_CREDENTIALS_ID}"]]])
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${env.DOCKER_IMAGE_NAME}:${env.DOCKER_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${env.DOCKER_CREDENTIALS_ID}") {
                        docker.image("${env.DOCKER_IMAGE_NAME}:${env.DOCKER_TAG}").push()
                    }
                }
            }
        }
    }
}

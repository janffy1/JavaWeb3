pipeline {
    agent any

    environment {
        IMAGE_NAME = 'yourdockerhubusername/java-calculator'
    }

    stages {
        stage('Clone Repo') {
            steps {
                // Clone your repo from GitHub
                git 'https://github.com/CeeyIT-Solutions/JavaWeb3.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    dockerImage = docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                // Login to Docker Hub using credentials stored in Jenkins
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    dockerImage.push()
                }
            }
        }
    }
}

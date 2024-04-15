pipeline {
    agent any

    tools {
        nodejs "nodejs-20"
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo "Checking out repository..."
                    sleep 1
                }
            }
        }

        stage('Dependency Installation') {
            steps {
                echo "Installing dependencies..."
                sleep 60
            }
        }

        stage('Initialize docker') {
            steps {
                script {
                    echo "Initializing Docker..."
                    sleep 2
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sleep 70
            }
        }

        stage('Run Docker Image') {
            steps {
                echo "Running Docker image..."
                sleep 15
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    echo "Logging in to Docker Hub..."
                    sleep 30
                    echo "Tagging Docker image..."
                    sleep 30
                    echo "Pushing Docker image..."
                    sleep 40
                }
            }
        }
    }
}

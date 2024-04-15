pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    sh '''
                    if [ ! -d "newDirectory" ]; then
                        echo "Cloning repository..."
                        git clone https://github.com/bilal-akbar-9/simple-reactjs-app.git newDirectory
                    fi
                    '''
                }
            }
        }

        stage('Dependency Installation') {
            steps {
                sh 'echo "Installing dependencies..."'
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'echo "Building Docker image..."'
                sh 'docker build -t simple-react-app .'
            }
        }

        stage('Run Docker Image') {
            steps {
                sh 'echo "Running Docker image..."'
                sh 'docker run -d -p 80:80 --name app-container simple-react-app'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                    echo "Logging in to Docker Hub..."
                    docker login -u $DOCKER_USER --password-stdin
                    docker tag simple-react-app:latest $DOCKER_USER/simple-react-app:latest
                    docker push $DOCKER_USER/simple-react-app:latest
                    '''
                }
            }
        }
    }
}

pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'pasindusheshan'   // change to your Docker Hub username
        FRONTEND_IMAGE = "${DOCKERHUB_USER}/simple-frontend:latest"
        BACKEND_IMAGE  = "${DOCKERHUB_USER}/spring-backend:latest"
    }

    stages {
        stage('Build') {
            steps {
                echo "Building Docker images..."
                sh 'docker build -t $FRONTEND_IMAGE ./frontend'
                sh 'docker build -t $BACKEND_IMAGE ./backend'
            }
        }

        stage('Push') {
            steps {
                echo "Pushing Docker images to Docker Hub..."
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $FRONTEND_IMAGE'
                    sh 'docker push $BACKEND_IMAGE'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying with Docker Compose..."
                sh 'docker-compose down || true'
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            echo "Pipeline finished!"
        }
    }
}

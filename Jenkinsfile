pipeline {
    agent any

    environment {
        IMAGE_NAME = 'docapp'
        CONTAINER_NAME = 'docapp-container'
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Run Migrations') {
            steps {
                echo 'Running migrations...'
                sh 'docker run --rm ${IMAGE_NAME}:latest python manage.py migrate'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                    docker run -d \
                        --name ${CONTAINER_NAME} \
                        -p 8000:8000 \
                        -e DEBUG=True \
                        -e ALLOWED_HOSTS=* \
                        --restart unless-stopped \
                        ${IMAGE_NAME}:latest
                '''
            }
        }

        stage('Health Check') {
            steps {
                echo 'Checking application health...'
                sh 'sleep 5 && docker ps | grep ${CONTAINER_NAME}'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! DocApp is running.'
        }
        failure {
            echo 'Deployment failed!'
            sh 'docker logs ${CONTAINER_NAME} || true'
        }
    }
}

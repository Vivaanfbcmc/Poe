pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "static-site:latest"
        CONTAINER_NAME = "static-site-container"
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo "Cloning repository..."
                git branch: 'main', url: 'https://github.com/Vivaanfbcmc/devops-assignment-8.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                bat """
                    docker build -t ${DOCKER_IMAGE} .
                """
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running Docker container..."
                bat """
                    docker rm -f ${CONTAINER_NAME} || exit 0
                    docker run -d --name ${CONTAINER_NAME} -p 9090:80 ${DOCKER_IMAGE}
                """
            }
        }
    }

    post {
        always {
            echo "Displaying all containers..."
            bat 'docker ps -a'
        }
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed. Please check the logs."
        }
    }
}

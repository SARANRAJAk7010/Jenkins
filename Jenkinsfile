pipeline {
    agent any

    environment {
        APP_NAME = "pyapp"
        APP_PORT = "5000"
    }

    stages {
        stage("Checkout Code") {
            steps {
                echo "Cloning code..."
                checkout scm
            }
        }

        stage("Build Docker Image") {
            steps {
                echo "Building Docker image..."
                sh "docker build -t ${APP_NAME}:latest ."
            }
        }

        stage("Run Container") {
            steps {
                echo "Running container..."
                sh """
                  docker rm -f ${APP_NAME} || true
                  docker run -d --name ${APP_NAME} -p ${APP_PORT}:5000 ${APP_NAME}:latest
                """
            }
        }

        stage("Test App") {
            steps {
                echo "Testing app..."
                sh "sleep 3"
                sh "curl -f http://localhost:${APP_PORT}/health"
                sh "curl -f http://localhost:${APP_PORT}/"
            }
        }
    }

    post {
        always {
            echo "Cleanup..."
            sh "docker rm -f ${APP_NAME} || true"
        }
    }
}


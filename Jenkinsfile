pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh '''
                    docker run --rm \
                      -v "$WORKSPACE:/app" \
                      -w /app \
                      python:3.12-slim \
                      sh -c "pip install -r app/requirements.txt && pytest app/"
                '''
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Docker build will be added next'
            }
        }
    }
}
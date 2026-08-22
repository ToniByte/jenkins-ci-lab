pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                deleteDir()

                git branch: 'main',
                    credentialsId: 'github-ssh',
                    url: 'git@github.com:tonibyte/jenkins-ci-lab.git'
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
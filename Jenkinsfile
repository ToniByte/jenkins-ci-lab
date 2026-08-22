pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                deleteDir()

                git branch: 'main',
                    credentialsId: 'github-ssh',
                    url: 'https://github.com/tonibyte/jenkins-ci-lab.git'
            }
        }

        stage('Test') {
            steps {
                sh '''
                    docker run --rm \
                      -v "$WORKSPACE/app:/app" \
                      -w /app \
                      python:3.12-slim \
                      sh -c "pip install -r requirements.txt && pytest"
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build \
                      -t jenkins-ci-app:${BUILD_NUMBER} \
                      .
                '''
            }
        }

        stage('Security Scan') {
            steps {
                sh '''
                    trivy image \
                      --severity HIGH,CRITICAL \
                      --exit-code 1 \
                      jenkins-ci-app:${BUILD_NUMBER}
                '''
            }
        }
    }
}
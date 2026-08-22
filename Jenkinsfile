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
            echo "=== Jenkins workspace ==="
            ls -la

            echo "=== app directory ==="
            ls -la app

            echo "=== Docker container ==="
            docker run --rm \
              -v "$WORKSPACE/app:/app" \
              -w /app \
              python:3.12-slim \
              sh -c "ls -la"
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
    }
}
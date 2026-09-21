pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Code has been checked out from GitHub'
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    echo "Building Docker image..."
                    docker build -t jenkins-demo:1.0 .
                '''
            }
        }

        stage('Docker Run') {
            steps {
                sh '''
                    echo "Starting Docker container..."

                    docker rm -f jenkins-demo || true

                    docker run -d \
                        --name jenkins-demo \
                        -p 8081:80 \
                        jenkins-demo:1.0

                    echo "Container started successfully!"
                '''
            }
        }
    }
}

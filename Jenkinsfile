pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Docker image...'

                sh '''
                    docker build -t jenkins-demo:1.0 .
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Docker image...'

                sh '''
                    docker run --rm jenkins-demo:1.0 nginx -t
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                sh '''
                    docker stop jenkins-demo || true
                    docker rm jenkins-demo || true

                    docker run -d \
                        --name jenkins-demo \
                        -p 8081:80 \
                        jenkins-demo:1.0
                '''
            }
        }
    }
}

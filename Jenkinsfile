pipeline {
    agent {
        docker {
            image 'node:16-alpine'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        DOCKER_IMAGE = "rgr-test_app:latest"
        CONTAINER_NAME = "test_app"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Deploy Application') {
            steps {
                script {
                    sh '''
                        npm install
                    '''
                }
            }
        }
    }
}

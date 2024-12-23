pipeline {
agent any
environment {
DOCKER_IMAGE = "rgr-test_app:latest"
CONTAINER_NAME = "test_app"
}
stages {
stage('Clone Repository') {
steps {
git branch: 'main', url: 'https://github.com/ertewi/jenkins_test'
}
}
stage('Build Docker Image') {
steps {
script {
sh '''
ls -la
docker --version
docker build -t $DOCKER_IMAGE .
'''
}
}
}
stage('Deploy Application') {
steps {
script {
sh '''
docker stop $CONTAINER_NAME || true
docker rm $CONTAINER_NAME || true
docker run -d --name $CONTAINER_NAME --network proxy -p 3000:3000 $DOCKER_IMAGE
'''
}
}
}
}
triggers {
pollSCM('H/5 * * * *')
}
}

pipeline {
    agent any
    environment{
        DOCKERHUB_CREDENTIALS = 'DOCKERHUB_CREDENTIALS'
        IMAGE_NAME = 'yoga3911/hello-world'
        IMAGE_TAG = '1.0.0'
    }
    stages {
        stage("Checkout Code") {
            steps {
                bat "echo 'Git Checkout Started'"
                git branch: 'master', credentialsId: 'Yoga-SSH', url: 'git@github.com:Yoga3911/go-test-api.git'
                bat "echo 'Git Checkout Finished'"
            }
        }     
        stage("Test Code"){
            steps {
                bat "echo 'Test Started'"
                bat "go test ./test"
                bat "echo 'Test Finished'"
            }
        }
        stage("Build Image"){
            steps {
                bat "echo 'Build Started'"
                bat "docker build -t yoga3911/hello-world ."
                bat "echo 'Build Finished'"
            }
        }
        stage("Push Image"){
            steps {
                bat "echo 'Push Image Started'"
                withCredentials([usernamePassword(credentialsId: DOCKERHUB_CREDENTIALS, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    // bat 'docker login -u $USERNAME -p $PASSWORD'
                    bat "echo 'docker login -u $USERNAME -p $PASSWORD'"
                    bat "docker push yoga3911/hello-world:$IMAGE_TAG"
                }
                bat "echo 'Push Image Finished'"
            }
        }
        stage("Pull Image"){
            steps {
                bat "echo 'Pull Image Started'"
                bat "docker pull yoga3911/hello-world:$IMAGE_TAG"
                bat "echo 'Pull Image Finished'"
            }
        }
        stage("Deploy"){
            steps {
                bat "echo 'Deploy Started'"
                bat "docker stop hello-world"
                bat "docker rm hello-world"
                bat "docker run --name=hello-world -d -p 3000:3000 yoga3911/hello-world:latest"
                bat "echo 'Deploy Finished'"
            }
        }
    }
}
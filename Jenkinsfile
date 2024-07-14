pipeline {
    agent any
    environment{
        // DOCKERHUB_CREDENTIALS = 'DOCKERHUB_CREDENTIALS'
        IMAGE_NAME = 'yoga3911/hello-world'
        IMAGE_TAG = '3.0.0'
        CONTAINER_NAME = 'hello-world'
        CONTAINER_PORT = '3000:3000'
    }
    stages {
        stage("Checkout Project") {
            steps {
                bat "echo 'Git Checkout Started'"
                git branch: 'master', credentialsId: 'Yoga-SSH', url: 'git@github.com:Yoga3911/go-test-api.git'
                bat "echo 'Git Checkout Finished'"
            }
        }     
        stage("Code Analysis"){
            steps {
                bat "echo 'Test Started'"
                bat "go test ./test"
                bat "echo 'Test Finished'"
            }
        }
        stage("Unit Test"){
            steps {
                bat "echo 'Test Started'"
                bat "go test ./test"
                bat "echo 'Test Finished'"
            }
        }
        stage("Build Image"){
            steps {
                bat "echo 'Build Started'"
                // bat "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                script {
                        docker.withRegistry("https://registry-1.docker.io/v2/", 'DOCKERHUB_CREDENTIALS') {
                        image = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")                  
                    }
                }
                bat "echo 'Build Finished'"
            }
        }
        stage("Push Image"){
            steps {
                bat "echo 'Push Image Started'"
                script {
                        docker.withRegistry("https://registry-1.docker.io/v2/", 'DOCKERHUB_CREDENTIALS') {
                        // docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()                    
                        image.push()                    
                        // image.push("latest")                    
                    }
                }
                // withCredentials([usernamePassword(credentialsId: DOCKERHUB_CREDENTIALS, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                //     bat "docker login -u ${USERNAME} -p ${PASSWORD}"
                //     bat "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                // }
                bat "echo 'Push Image Finished'"
            }
        }
        stage("Pull Image"){
            steps {
                bat "echo 'Pull Image Started'"
                // bat "docker pull ${IMAGE_NAME}:${IMAGE_TAG}"
                script {
                        docker.withRegistry("https://registry-1.docker.io/v2/", 'DOCKERHUB_CREDENTIALS') {
                        image.pull()                    
                    }
                }
                bat "echo 'Pull Image Finished'"
            }
        }
        stage("Deploy"){
            steps {
                bat "echo 'Deploy Started'"
                catchError {
                    bat "docker stop ${CONTAINER_NAME}"
                    bat "docker rm ${CONTAINER_NAME}"
                }
                // bat "docker run --name=${CONTAINER_NAME} -d -p ${CONTAINER_PORT} ${IMAGE_NAME}:${IMAGE_TAG}"
                script {
                        docker.withRegistry("https://registry-1.docker.io/v2/", 'DOCKERHUB_CREDENTIALS') {
                        image.run("--name=${CONTAINER_NAME} -d -p ${CONTAINER_PORT}")                  
                    }
                }
                bat "echo 'Deploy Finished'"
            }
        }
    }
}
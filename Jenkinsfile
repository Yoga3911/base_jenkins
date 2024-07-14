pipeline {
    agent any
    stages {
        stage("Checkout"){
            steps {
                bat "echo 'Git Checkout Started'"
                git branch: 'master', credentialsId: 'Yoga-SSH', url: 'git@github.com:Yoga3911/go-test-api.git'
                bat "echo 'Git Checkout Finished'"
            }
        }     
        stage("Test"){
            steps {
                bat "echo 'Test Started'"
                bat "go test ./test"
                bat "echo 'Test Finished'"
            }
        }
        stage("Build"){
            steps {
                bat "echo 'Build Started'"
                bat "docker build -t yoga3911/hello-world ."
                bat "echo 'Build Finished'"
            }
        }
        stage("Deploy"){
            steps {
                bat "echo 'Deploy Started'"
                bat "docker run --name=hello-world -d -p 3000:3000 yoga3911/hello-world:latest"
                bat "echo 'Deploy Finished'"
            }
        }
    }
}
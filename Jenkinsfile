pipeline {
    agent any
    stages {
        stage("Checkout"){
            steps {
                git branch: 'master', credentialsId: 'Yoga-SSH', url: 'git@github.com:Yoga3911/go-test-api.git'
            }
        }     
        stage("Build"){
            steps {
                bat "docker build -t yoga3911/hello-world ."
            }
        }
        stage("Deploy"){
            steps {
                bat "echo 'Deploying the application'"
            }
        }
    }
}
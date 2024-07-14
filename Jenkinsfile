pipeline {
    agent any
    stages {
        stage("Checkout"){
            steps {
                git branch: 'master', credentialsId: 'SSH', url: 'https://github.com/Yoga3911/go-test-api'
            }
        }     
        stage("Build"){
            steps {
                sh "docker build -t yoga3911/hello-world ."
            }
        }
        stage("Deploy"){
            steps {
                sh "echo 'Deploying the application'"
            }
        }
    }
}
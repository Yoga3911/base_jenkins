pipeline {
    stages {
        stage("Checkout"){
            steps {
                git branch: 'master', credentialsId: 'GitHub-Yoga3911', url: 'https://github.com/Yoga3911/go-test-api'
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
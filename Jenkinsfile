pipeline {

    agent {
        docker {
            image 'bryandollery/alpine-docker'
        }
    }
    stages {
        stage ('generate manifest') {
            steps {
                sh "echo 'time' $(date) > manifest.txt"
                sh "echo 'build number: ' $BUILD_NUMBER >> manifest.txt"
            }
        }
        stage ('build') {
            steps {
                sh "docker build --tag manifest-holder:latest ."
            }
        }
    }
} 

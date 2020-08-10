pipeline {

    agent {
        docker {
            image 'bryandollery/alpine-docker'
        }
    }
    stages {
        stage ('generate manifest') {
            steps {
                sh "echo 'time' ${BUILD_ID} > manifest.txt"
                sh "echo 'build number: ' ${BUILD_NUMBER} >> manifest.txt"
            }
        }
        stage ('build') {
            steps {
                sh "docker build --tag manifest-holder:latest ."
            }
        }
        stage ('test') {
            steps {
                sh "docker run -it --rm manifest-holder"
            }
        }
    }
} 

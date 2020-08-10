pipeline {

    agent {
        docker {
            image 'bryandollery/alpine-docker'
        }
    }
    stages {
        stage ('generate manifest') {
            steps {
                sh """
echo <<EOF > ./manifest.txt
time: ${BUILD_ID}
build #: ${BUILD_NUMBER}
EOF
cat ./manifest.txt
pwd
ls -gAlFh
"""
            }
        }
        stage ('build') {
            steps {
                sh "cat ./manifest.txt"
                sh "docker build --tag manifest-holder:latest ."
            }
        }
        stage ('test') {
            steps {
                sh "docker run --rm manifest-holder"
            }
        }
    }
} 

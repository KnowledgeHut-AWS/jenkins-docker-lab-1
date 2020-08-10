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
cat <<EOF > ./manifest.txt
name: ${JOB_NAME}
time: ${currentBuild.startTimeInMillis}
build #: ${BUILD_NUMBER}
commit: ${GIT_COMMIT}
url: ${GIT_URL}
author: ${GIT_AUTHOR_NAME} (${GIT_AUTHOR_EMAIL})
EOF
"""
            }
        }
        stage ('build') {
            steps {
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

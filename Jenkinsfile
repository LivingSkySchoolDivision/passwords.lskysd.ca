pipeline {
    agent any
    environment {
        DOCKERREPO = 'utilitywebsites/passwords.lskysd.ca'
        FULL_DOCKER_REPO = "${PRIVATE_DOCKER_REGISTRY}/${DOCKERREPO}"
        TAG = "${BUILD_TIMESTAMP}"
    }
    stages {
        stage('Git clone') {
            steps {
                git branch: 'master',
                    url: "https://sourcecode.lskysd.ca/PublicCode/passwords.lskysd.ca.git"
            }
        }
        stage('Docker build') {
            steps {
                sh "docker build --no-cache -t ${FULL_DOCKER_REPO}:latest -t ${FULL_DOCKER_REPO}:${TAG} ."
            }
        }
        stage('Docker push') {
            steps {
                sh "docker push ${FULL_DOCKER_REPO}:${TAG}"
                sh "docker push ${FULL_DOCKER_REPO}:latest"
            }
        }
    }
    post {
        always {
            deleteDir()
        }
    }
}


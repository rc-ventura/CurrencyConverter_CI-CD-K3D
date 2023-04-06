pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                        dockerImage = docker.build("-f Dockerfile -t ${DOCKER_REGISTRY}/currency-converter-backend:${env.BUILD_ID} .")
                }
            }
        }
        stage ('Push Docker Image'){
            steps {
                script {
                    docker.withRegistry("https://registry.hub.docker.com", "dockerhub-credentials") {
                        dockerImage.push('${env.BUILD_ID}')
                        dockerImage.push('latest')                    }
                }
            }
        }
    }
}


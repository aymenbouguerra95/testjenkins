pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "aymenbouguerra/myapp"
        DOCKER_TAG   = "latest"
        DOCKER_HOST  = "tcp://host.docker.internal:2375" // TCP Docker على Windows
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker -H $DOCKER_HOST build -t $DOCKER_IMAGE:$DOCKER_TAG ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "docker -H $DOCKER_HOST login -u $DOCKER_USER -p $DOCKER_PASS"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker -H $DOCKER_HOST push $DOCKER_IMAGE:$DOCKER_TAG"
            }
        }
    }
}

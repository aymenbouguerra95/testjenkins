pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "aymenbouguerra/myapp"
        DOCKER_TAG   = "latest"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t $DOCKER_IMAGE:$DOCKER_TAG ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push $DOCKER_IMAGE:$DOCKER_TAG"
            }
        }
    }
}

pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Build Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%IMAGE_TAG% ."
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat "kubectl config use-context docker-desktop"
                bat "kubectl set image deployment/cicd-app cicd-app=%IMAGE_NAME%:%IMAGE_TAG% --record"
                bat "kubectl rollout status deployment/cicd-app"
            }
        }
    }
}
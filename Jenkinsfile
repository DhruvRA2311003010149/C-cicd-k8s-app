pipeline {
    agent any

    environment {
        KUBECONFIG = "C:\\Users\\Dhruv\\.kube\\config"
        IMAGE_NAME = "cicd-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Build Image') {
            steps {
                bat "docker build --no-cache -t %IMAGE_NAME%:%IMAGE_TAG% ."
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat "kubectl --kubeconfig=%KUBECONFIG% config use-context docker-desktop"
                bat "kubectl --kubeconfig=%KUBECONFIG% set image deployment/cicd-app cicd-app=%IMAGE_NAME%:%IMAGE_TAG%"
                bat "kubectl --kubeconfig=%KUBECONFIG% rollout status deployment/cicd-app"
            }
        }
    }
}
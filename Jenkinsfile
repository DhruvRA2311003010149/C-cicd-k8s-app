pipeline {
    agent any

    environment {
        KUBECONFIG = "C:\\Users\\Dhruv\\.kube\\config"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build --no-cache -t cicd-app:latest .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl config use-context docker-desktop'
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml --validate=false'
                bat 'kubectl delete pod -l app=cicd-app'
            }
        }
    }
}
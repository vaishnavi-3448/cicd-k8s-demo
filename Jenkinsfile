pipeline {
    agent any

    environment {
        KUBECONFIG = 'C:\\Users\\user\\.kube\\config'
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t cicd-k8s-demo:latest .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s\\deployment.yaml --validate=false'
                bat 'kubectl apply -f k8s\\service.yaml --validate=false'
            }
        }

        stage('Restart Deployment') {
            steps {
                bat 'kubectl rollout restart deployment cicd-k8s-deployment'
            }
        }

        stage('Verify') {
            steps {
                bat 'kubectl get pods'
                bat 'kubectl get svc'
            }
        }
    }
}
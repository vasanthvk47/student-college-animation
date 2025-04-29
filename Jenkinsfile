pipeline {
    agent any

    environment {
        IMAGE_NAME = "vasanth4747/student-college-animation"
        TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vasanthvk47/student-college-animation.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME:$TAG ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Skip Docker login and push directly, assuming login is already done manually
                script {
                    sh "docker push $IMAGE_NAME:$TAG"
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh "kubectl apply -f k8s/deployment.yaml"
                    sh "kubectl apply -f k8s/service.yaml"
                }
            }
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/sarvesh-8393/devops_project'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t sarvesh8393/devops-mini:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push sarvesh8393/devops-mini:latest'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}

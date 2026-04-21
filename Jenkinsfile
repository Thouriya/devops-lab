pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Thouriya/devops-lab.git', branch: 'main'
            }
        }

        stage('Build Docker') {
            steps {
                sh 'docker build -t webapp:latest .'
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }
    }
}

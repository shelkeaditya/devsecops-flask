pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/shelkeaditya/devsecops-flask-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devsecops-demo .'
            }
        }

        stage('Security Scan - Trivy') {
            steps {
                sh 'trivy image --severity HIGH,CRITICAL devsecops-demo || true'
            }
        }

        stage('Deploy Locally') {
            steps {
                sh 'docker run -d -p 5000:5000 --name devsecops-app devsecops-demo || true'
            }
        }
    }
}


pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "devops-backend"
        FRONTEND_IMAGE = "devops-frontend"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/shaiksalmanmca1/Devops-CI-CD.git'
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                dir('backend') {
                    sh 'docker build -t $BACKEND_IMAGE .'
                }
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                dir('frontend') {
                    sh 'docker build -t $FRONTEND_IMAGE .'
                }
            }
        }

        stage('Run Backend Container') {
            steps {
                sh 'docker rm -f backend || true'
                sh 'docker run -d -p 8081:8080 --name backend $BACKEND_IMAGE'
            }
        }

        stage('Run Frontend Container') {
            steps {
                sh 'docker rm -f frontend || true'
                sh 'docker run -d -p 3000:80 --name frontend $FRONTEND_IMAGE'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! Backend on port 8081, Frontend on port 3000'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}

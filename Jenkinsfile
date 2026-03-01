pipeline {
    agent any

    environment {
        IMAGE_NAME = "cythonvijay/vijay-devops-site"
        CONTAINER_NAME = "devops-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'git@github.com:cythonvijay/vijay-devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d -p 8081:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                docker ps
                '''
            }
        }

    }

    post {
        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}

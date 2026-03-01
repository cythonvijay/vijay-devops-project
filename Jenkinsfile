pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'git@github.com:cythonvijay/vijay-devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cythonvijay/vijay-devops-site .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop devops-container || true
                docker rm devops-container || true
                docker run -d -p 8081:80 --name devops-container cythonvijay/vijay-devops-site
                '''
            }
        }

    }
}

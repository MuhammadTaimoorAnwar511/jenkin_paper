pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/aditya-sridhar/simple-reactjs-app.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('taimooranwar/simple-reactjs-app:latest')
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    docker.image('taimooranwar/simple-reactjs-app:latest').run()
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', dockerhub-credentials) {
                        docker.image('taimooranwar/simple-reactjs-app:latest').push()
                    }
                }
            }
        }
    }
}

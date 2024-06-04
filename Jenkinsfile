pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                git url: 'https://github.com/MuhammadTaimoorAnwar511/jenkin_paper.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install dependencies using npm
                bat 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    docker.build("taimooranwar/simple-reactjs-app:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Run Docker Image') {
            steps {
                // Run Docker container
                script {
                    docker.image("taimooranwar/simple-reactjs-app:${env.BUILD_NUMBER}").inside('-d -p 3000:3000') {
                        echo 'Docker container is running'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                // Push Docker image to Docker Hub
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image("taimooranwar/simple-reactjs-app:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}

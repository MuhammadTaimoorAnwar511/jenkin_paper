pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MuhammadTaimoorAnwar511/jenkin_paper.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                bat 'npm install' // Use bat for running Windows batch commands
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Change to the directory containing the Dockerfile
                    dir('C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Simple ReactJS App Pipeline') {
                        docker.build('taimooranwar/simple-reactjs-app:latest')
                    }
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
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image('taimooranwar/simple-reactjs-app:latest').push()
                    }
                }
            }
        }
    }
}

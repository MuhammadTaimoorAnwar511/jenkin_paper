pipeline {
    agent any

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
                sh 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    def app = docker.build("taimooranwar/simple-reactjs-app")
                }
            }
        }
        stage('Run Docker Image') {
            steps {
                // Run Docker container
                script {
                    def app = docker.build("taimooranwar/simple-reactjs-app")
                    app.run('-d -p 3000:3000')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                // Push Docker image to Docker Hub
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        def app = docker.build("taimooranwar/simple-reactjs-app")
                        app.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }
    }
}

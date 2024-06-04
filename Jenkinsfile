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
                    def dockerfilePath = findDockerfile()
                    if (dockerfilePath) {
                        dir(dockerfilePath.parent) {
                            docker.build('taimooranwar/simple-reactjs-app:latest')
                        }
                    } else {
                        error('Dockerfile not found!')
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

def findDockerfile() {
    def dockerfile = findFiles(glob: '**/Dockerfile')
    if (dockerfile) {
        return dockerfile[0]
    } else {
        return null
    }
}

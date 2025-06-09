pipeline {
    agent any

    environment {
        IMAGE_NAME = 'shannu/myapp'        // Change to your Docker Hub repo name
        CONTAINER_NAME = 'myapp-container'
        DOCKER_CREDENTIALS_ID = 'dockerhub-creds' // Jenkins credentials ID
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'git branch: 'main', url: 'https://github.com/shannu0188/self-project.git''
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${SHANNU}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        docker.image("${SHANNU}:latest").push()
                    }
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh "docker rm -f ${SHANNU} || true"
                    sh "docker run -d -p 3000:3000 --name ${myapp-container} ${SHANNU}:latest"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}

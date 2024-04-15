pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/your-image-name'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/aditya-sridhar/simple-reactjs-app?tab=readme-ov-file'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                sh 'docker run -d -p 80:80 ${env.DOCKER_IMAGE}'
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image(env.DOCKER_IMAGE).push('latest')
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
    }
}

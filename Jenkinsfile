pipeline {
    agent any

    environment {
        // Define your Docker image name directly in the pipeline environment settings
        DOCKER_IMAGE = 'your-dockerhub-username/your-image-name'
    }

    stages {
        stage('Checkout') {
            steps {
                // Cloning the code from GitHub
                git 'https://github.com/GitUsmanBaig/simple-reactjs-app'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Installing project dependencies
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Building a Docker image from the Dockerfile located in the project root directory
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                // Running the Docker image in a detached mode on port 80
                sh 'docker run -d -p 80:80 ${env.DOCKER_IMAGE}'
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Logging in to Docker Hub and pushing the Docker image
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

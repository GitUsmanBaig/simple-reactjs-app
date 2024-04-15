pipeline {
    agent any

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
                dir('simple-reactjs-app') {
                    script {
                        // Building a Docker image from the Dockerfile in the project root directory
                        sh "docker build . -t simple-reactjs-app ."
                    }
                }
            }
        }


        stage('Run Docker Image') {
            steps {
                // Running the Docker image in a detached mode on port 80
                sh "docker run -d -p 80:80 simple-reactjs-app"
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Logging into Docker Hub and pushing the Docker image
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        sh "docker push simple-reactjs-app"
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

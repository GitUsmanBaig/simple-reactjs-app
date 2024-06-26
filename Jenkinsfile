pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/GitUsmanBaig/simple-reactjs-app'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('simple-reactjs-app') {
                    script {
                        sh "docker build -t simple-reactjs-app ."
                    }
                }
            }
        }


        stage('Run Docker Image') {
            steps {
                sh "docker run -d -p 80:80 simple-reactjs-app"
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
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

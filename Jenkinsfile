pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/<your_username>/<repository_name>.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-react-app .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 3000:3000 my-react-app'
            }
        }
        stage('Verify') {
            steps {
                sh 'sleep 10' // Wait for container to start
                sh 'curl http://localhost:3000' // Verify app is running
            }
        }
    }
}

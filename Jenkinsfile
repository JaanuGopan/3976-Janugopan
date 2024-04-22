pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/JaanuGopan/3976-Janugopan.git'
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

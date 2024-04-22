pipeline {
    agent any

    parameters {
        string(name: 'GIT_URL', defaultValue: 'https://github.com/JaanuGopan/3976-Janugopan.git', description: 'GitHub repository URL')
        string(name: 'GIT_BRANCH', defaultValue: 'main', description: 'Git branch')
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${params.GIT_BRANCH}", url: "${params.GIT_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    try {
                        sh 'docker build -t my-react-app .'
                    } catch (Exception e) {
                        echo "Failed to build Docker image: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Failed to build Docker image")
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    try {
                        sh 'docker run -d -p 3000:3000 my-react-app'
                    } catch (Exception e) {
                        echo "Failed to run Docker container: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Failed to run Docker container")
                    }
                }
            }
        }

        stage('Verify') {
            steps {
                script {
                    try {
                        sh 'sleep 10' // Wait for container to start
                        sh 'curl http://localhost:3000' // Verify app is running
                    } catch (Exception e) {
                        echo "Failed to verify application: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Failed to verify application")
                    }
                }
            }
        }

        stage('Cleanup') {
            steps {
                sh 'docker stop $(docker ps -q --filter ancestor=my-react-app)'
                sh 'docker rm $(docker ps -a -q --filter ancestor=my-react-app)'
            }
        }
    }
}

pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-project"
        CONTAINER_NAME = "my-first-project"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Bhanu231003/Docker-files.git',
                    credentialsId:'docker-creds'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                "C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" build -t %IMAGE_NAME%:latest .
                 
                '''
            }
        }

        stage('Stop Old Container') {
            steps {
                bat '''
                "C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" docker stop %CONTAINER_NAME% || exit 0  docker rm %CONTAINER_NAME% || exit 0
                
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" run --detach -p 6999:80 --name %CONTAINER_NAME% %IMAGE_NAME%:latest'''
                
                
            }
        }
    }

    post {
        success {
            echo "🚀 Docker container deployed successfully on Windows!"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}
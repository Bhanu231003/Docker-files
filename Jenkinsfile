pipeline {
    agent any
    
    environment {
        registry = "bhanu180/docker"  // Your Docker Hub repo
        registryCredential = 'dockerhub-creds'  // Create this credential in Jenkins
        dockerImage = ''
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Works in Pipeline from SCM / Multibranch
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }
        
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', registryCredential) {
                        dockerImage.push()
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
    
    post {
        always {
            script {
                if (dockerImage) {
                    sh "docker rmi ${registry}:${BUILD_NUMBER} || true"
                    sh "docker rmi ${registry}:latest || true"
                }
            }
        }
    }
}
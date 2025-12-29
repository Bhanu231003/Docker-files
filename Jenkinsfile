pipeline {
    agent { 
        label 'docker-agent'  // Use node labeled 'docker-agent'
    }
    
    environment {
        registry = "bhanu180/docker"
        registryCredential = 'dockerhub-creds'
        dockerImage = ''
    }
    
    stages {
        stage('Checkout') { steps { checkout scm } }
        
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
}
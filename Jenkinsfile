pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/tharinduk001/GitHub-Docker-and-Jenkins-CI-CD-Pipeline.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t kalharacodes/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
              withCredentials([string(credentialsId: 'dockerpassword', variable: 'DockerPasswordVariable')]) {
        script {
                bat "docker login -u kalharacodes -p %DockerPasswordVariable%"
            }
            }        
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push kalharacodes/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}

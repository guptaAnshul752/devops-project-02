pipeline {
    agent any
    
    environment{
        dockercredentials=credentials('dockerhub') 
    }
    
    stages {
        
        stage('Build & Package spring app') {
            steps {
                dir('springboot-backend') {
                  bat 'mvn clean install -DskipTests'
                }
            }
        }

        stage('Build images of both app') {
            steps {
                dir('springboot-backend') {
                  bat 'docker build -t springboot-backend:1.0 .'
                }
                
                dir('react-frontend') {
                  bat 'docker build -t react-frontend:1.0 .'
                }
                
            }
        }
        
        stage('Push images to hub') {
            steps {
                bat 'echo $dockercredentials_PSW | docker login -u $dockercredentials_USR --password-stdin '
                bat 'docker image tag springboot-backend:1.0 guptaanshul752/springboot-backend:1.0'
                bat 'docker image push guptaanshul752/springboot-backend:$BUILD_NUMBER'
                
                bat 'docker image tag react-frontend:0.1 guptaanshul752/react-frontend:1.0'
                bat 'docker image push guptaanshul752/react-frontend:1.0'
            }
        }
    }
}

pipeline {
    agent any
    
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
                  bat 'docker build -t springboot-backend:$BUILD_NUMBER .'
                }
                
                dir('react-frontend') {
                  bat 'docker build -t react-frontend:$BUILD_NUMBER .'
                }
                
            }
        }
    }
}

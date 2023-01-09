pipeline {
    agent any
    
    tools{
        maven '3.8.6'
        nodejs '16.10.0'
    }
    
    stages {
        
        stage('Build & Package spring app') {
            steps {
                dir('springboot-backend') {
                  sh 'mvn clean '
                  sh 'mvn install -DskipTests '
                }
            }
        }

        stage('Build images of both app') {
            steps {
                dir('springboot-backend') {
                  sh 'docker build -t springboot-backend:$BUILD_NUMBER . '
                }
                
                dir('react-frontend') {
                  sh 'docker build -t react-frontend:$BUILD_NUMBER . '
                }
                
            }
        }
    }
}

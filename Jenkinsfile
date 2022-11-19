pipeline {
    agent any

    stages {
        stage('clean-image') {
            steps {
               sh '''
               docker rm -rf $(docker ps -aq)
               '''
            }
        }
       stage('build image') {
            steps {
               sh '''
                docker build -t eric:001 .
               '''
            }
        }
       stage('checking images') {
            steps {
               sh '''
               docker images 
               '''
            }
        }
    
       stage('launch container') {
            steps {
               sh '''
               docker run -i --name eric:001
               '''
            }
        }
     
    }


}

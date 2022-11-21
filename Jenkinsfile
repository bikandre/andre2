pipeline {
    agent any
    options {
    buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '30'))
  }
    stages {
        stage('clean-image') {
            steps {
               sh '''
               docker rm -f $(docker ps -aq)
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

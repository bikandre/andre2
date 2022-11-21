pipeline {
    agent any
    options ([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '',
     daysToKeepStr: '2', numToKeepStr: '5')), disableConcurrentBuilds()])
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

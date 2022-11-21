pipeline {
    agent any
    options {
    buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '30'))
  }

     environment {
        USERNAME = 'devopseasylearning2021'
        PASSWORD = 'Dev0ps2021@'
  }

    stages {
        stage('clean-image') {
            steps {
               sh '''
               docker ps
               '''
            }
        }
       stage('build image') {
            steps {
               sh '''
                docker build -t andrejenkins001 .
               '''
            }
        }
       stage('docker login') {
            steps {
               sh '''
               docker tag andrejenkins001 devopseasylearning2021/s3andre:andrejenkins001
               '''
            }
       
       stage('docker login') {
            steps {
               sh '''
               docker login -u $USERNAME -p $PASSWORD
               '''
            }
        }
    
       stage('docker push') {
            steps {
               sh '''
               docker push devopseasylearning2021/s3andre:jenkins001
               '''
            }
        }
     
    }


   }

}


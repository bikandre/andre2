pipeline {
    agent any
    options {
    buildDiscarder(logRotator(numToKeepStr: '3', artifactNumToKeepStr: '1'))
  }
     environment {
       DOCKERHUB_CREDENTIALS=credentials('dockerhub')
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
       stage('docker tag') {
            steps {
               sh '''
               docker tag andrejenkins001 devopseasylearning2021/s3andre:andrejenkins001 
               '''
            }
        }

       stage('docker login') {
            steps {
                    sh 'echo "${password} | docker login -u ${username} --password-stdin'
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

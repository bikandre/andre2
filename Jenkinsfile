pipeline {
    agent any
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '2', numToKeepStr: '5')), disableConcurrentBuilds()])
    stages {
        stage('clean-image') {
            steps {
               sh '''
               ls
               pwd
               '''
            }
        }
       stage('build image') {
            steps {
               sh '''
                touch s3andre
               '''
            }
        }
       stage('checking images') {
            steps {
               sh '''
               cat s3andre 
               '''
            }
        }
    
       stage('launch container') {
            steps {
               sh '''
               mv s3andre s3dre
               '''
            }
        }
     
    }


}

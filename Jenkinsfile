pipeline {
    agent any
    options {
    buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '30'))
  }

     environment {
       DOCKERHUB_CREDENTIALS=credentials('dockerhub')
  }
    parameters {
     string (name: 'clusterName', defaultValue: 'eks', description: 'Name of deploying cluster')
     string (name: 'region', defaultValue: 'Atlanta south', description: 'AWS region to execute command')
     string (name: 'chartName', defaultValue: '', description: 'the name of the chart you want to dry run')
     string (name: 'nameSpace', defaultValue: '', description: 'the nameSpace of deployment')
     choice choices: ['local', 'remote'], description: 'environments', name: 'deploySource'
     choice choices: ['dev', 'test', 'preprod', 'prod'], description: 'environments', name: 'env'  
     choice choices: ['Nelly', 'Juan', 'Andre', 'Idris'], description: 'Make your choice', name: 'ektech'
     booleanParam description: 'enter your cluster', name: 'which cluster'
    }
    stages { 
        stage('printing parameters') {
            steps {
                script {
                    sh """
                    echo 'clusterName: ${params.clusterName}'
                    echo 'region is: ${params.region}'
                    echo 'chartName is: ${params.chartName}'
                    echo 'nameSpace is: ${params.nameSpace}'
                    echo 'deploySource is: ${params.deploySource}'
                    echo 'deployMode is: ${params.deployMode}'
                    echo 'normalchart is: ${params.normalchart}'
                    echo 'deployWithSecret is: ${params.env}'
                    """
                }
            }
        }
        stage('clean-image') {
            steps {
                sh'''
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
                script {
               if (params.env == 'dev') {
                  sh """
                  echo 'This is a ${params.env} environment'
                  echo 'Deploying into ${params.env} environment =========================='
                  docker tag andrejenkins001 devopseasylearning2021/s3andre:andrejenkins001 
                  """
                }  
            }
        }
     }
       stage('docker login') {
            steps {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

       stage('docker push') {
            steps {
               sh '''
               docker push devopseasylearning2021/s3andre:andrejenkins001
               '''
            }
        }
     
    }


  }

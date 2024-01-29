pipeline {
    agent any
    environment{
        ENV_URL  = "pipeline.learning.com"  
    }
    stages{
        stage('stage Name-1'){
            steps{
                sh 'echo This is Jenkins pipeline'
            }
        }
        stage('stage Name-2'){
            steps{
                sh '''echo This is Demo 
                      echo This is Demo on Jenkins pipeline
                      echo printing '''
            }
        }
        stage('stage Name'){
            steps{
                sh "echo ${ENV_URL}"
            }
        }
    }
}

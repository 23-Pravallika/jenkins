pipeline {
    agent any
    environment{
        ENV_URL  = "pipeline.learning.com"    // Declaring pipeline at Pipeline level
    }
    stages{
        stage('stage Name-1'){
            steps{
                sh 'echo This is Jenkins pipeline'
            }
        }
        stage('stage Name-2'){
            environment{
                ENV_URL  = "stage.learning.com"   // Declaring pipeline at stage level
            }
            steps{
                sh "echo $ENV_URL"
            }
        }
        stage('stage Name'){
            steps{
                sh "echo ${ENV_URL}"
            }
        }
    }
}

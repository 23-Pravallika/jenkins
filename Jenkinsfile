pipeline {
    agent any
    environment{
        ENV_URL  = "pipeline.learning.com"    // Declaring pipeline at Pipeline level
    }
    // triggers { cron('*/1 * * * *') }
    triggers {pollSCM('*/1 * * * *')}
    tools {
        maven 'mvn' 
    }

    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Mr.Jenkins', description: 'Who should I say hello to?')

    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }
    stages{
        stage('stage Name-1'){
            steps{
                sh 'echo This is Jenkins pipeline'
                sh "echo ${ENV_URL}"
            }
        }
        stage('stage Name-2'){
            environment{
                ENV_URL  = "stage.learning.com"   // Declaring pipeline at stage level
            }
            steps{
                sh "echo ${ENV_URL}"
            }
        }
        stage('stage Name'){
            steps{
                sh "echo ${ENV_URL}"
            }
        }
        stage('checking maven commands'){
            steps{
                sh 'mvn clean'
            }
        }
    }
}

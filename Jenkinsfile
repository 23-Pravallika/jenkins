pipeline {
    agent {label 'Jenkins-WS'}
    
    environment{                             // all the sensitive info are mentioned under this environment
        ENV_URL  = "pipeline.learning.com"    // Declaring pipeline at Pipeline level
        SSH_CRED = credentials('SSH_CREDS')
    }

    // triggers { cron('*/1 * * * *') }
    // triggers {pollSCM('*/1 * * * *')}

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
                sh 'env'
                sh 'cd /home/centos/Jenkins-Node'
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
        stage('maven commands'){
            steps{
                sh 'mvn --version'
            }
        }
        stage('Using When'){
            when {
                branch 'dev'
            }
            steps{
                sh 'echo Deploying'
            }
        }
        stage('When with allOf'){
            when{
                allOf {                    //allOf Execute the stage when all of the nested conditions are true. Must contain at least one condition.
                    branch 'qa'
                    environment name: 'DEPLOY_TO', value: 'qa'
                }
            }
            steps{
                sh 'echo Deploying on Qa'
            }
        }
        stage('When with anyof'){
            when{
                anyOf {                  //anyOf Execute the stage when at least one of the nested conditions is true. Must contain at least one condition.
                    branch 'dev'
                    environment name: 'DEPLOY_TO', value: 'dev'
                }
            }
            steps{
                sh 'echo Deploying on dev'
            }
        }
        stage('Example on parallel stages') {
            parallel {
                stage('One') {
                    steps {
                    
                       sh "echo STAGE One in parallel stages"
                       sh "sleep 10"
                    }
                }
                stage('Two') {
                    steps {
                        sh "echo STAGE TWO in parallel stages"
                        sh "sleep 10"
                        sh "echo Printing 2"
                    }
                }
                stage('Three') {
                    steps {
                        sh "echo STAGE Three in parallel stages"
                        sh "sleep 10"
                        sh "echo Printing 3"
            }
        }
    }
}
    }
}
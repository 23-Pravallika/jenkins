pipeline {
    agent {label 'Jenkins-WS'} 
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select The Environment')
    }
    options {
        ansiColor('xterm')    // Add's color to the output : Ensure you install AnsiColor Plugin.
    }
    stages{
        stage('Destroying shipping'){
            steps{
                dir('shipping'){ git(branch: 'main', url: 'https://github.com/23-Pravallika/shipping.git')
                    sh '''
                            cd mutable-Infra
                            terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars
                            terraform destroy -var-file=${ENV}-env/${ENV}.tfvars  -var APP_VERSION=0.0.1 -auto-approve
                    '''
                }
            }
        }
        stage('Destroying User'){
            steps{
                dir('User'){ git(branch: 'main', url: 'https://github.com/23-Pravallika/user.git')
                    sh '''
                            cd mutable-Infra
                            terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars
                            terraform destroy -var-file=${ENV}-env/${ENV}.tfvars  -var APP_VERSION=0.0.2 -auto-approve
                    '''
                }
            }
        }
        stage('Destroying Catalogue'){
            steps{
                dir('Catalogue'){ git(branch: 'main', url: 'https://github.com/23-Pravallika/catalogue.git')
                    sh '''
                            cd mutable-Infra
                            terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars
                            terraform destroy -var-file=${ENV}-env/${ENV}.tfvars  -var APP_VERSION=0.0.2 -auto-approve
                    '''
                }
            }
        }
        // stage('Destroying Payment'){
        //     steps{
        //         dir('Payment'){ git(branch: 'main', url: 'https://github.com/23-Pravallika/payment.git')
        //             sh '''
        //                     cd mutable-Infra
        //                     terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars
        //                     terraform destroy -var-file=${ENV}-env/${ENV}.tfvars  -var APP_VERSION=0.0.1 -auto-approve
        //             '''
        //         }
        //     }
        // }
        stage('Destroying Cart'){
            steps{
                dir('Cart'){ git(branch: 'main', url: 'https://github.com/23-Pravallika/cart.git')
                    sh '''
                            cd mutable-Infra
                            terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars
                            terraform destroy -var-file=${ENV}-env/${ENV}.tfvars  -var APP_VERSION=0.0.1 -auto-approve
                    '''
                }
            }
        }
        stage('Destroying Frontend'){
            steps{
                dir('Frontend'){ git(branch: 'main', url: 'https://github.com/23-Pravallika/frontend.git')
                    sh '''
                            cd mutable-Infra
                            terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars
                            terraform destroy -var-file=${ENV}-env/${ENV}.tfvars  -var APP_VERSION=0.0.1 -auto-approve
                    '''
                }
            }
        }
        stage('Terraform Destroy Databases'){
            steps{
                git branch: 'main', url: 'https://github.com/23-Pravallika/terraform-dbs.git'
                    sh "terrafile -f ${ENV}-env/Terrafile"
                    sh "terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars"
                    sh "terraform destroy -var-file=${ENV}-env/${ENV}.tfvars -auto-approve"
            }
        }
        stage('Terraform Destroy alb'){
            steps{
                git(branch: 'main', url: ' https://github.com/23-Pravallika/tf-loadbalancers.git')
                    sh "terrafile -f ${ENV}-env/Terrafile"
                    sh "terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars"
                    sh "terraform destroy -var-file=${ENV}-env/${ENV}.tfvars -auto-approve"
            }
        }
        stage('Terraform Destroy Network'){
            steps{
                git branch: 'main', url: 'https://github.com/23-Pravallika/tf-vpc.git'
                    sh "terrafile -f ${ENV}-env/Terrafile"
                    sh "terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars"
                    sh "terraform destroy -var-file=${ENV}-env/${ENV}.tfvars -auto-approve"
            }
        }
    }
}




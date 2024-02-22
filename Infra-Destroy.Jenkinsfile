pipeline {
    agent {label 'Jenkins-WS'} 
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select The Environment')
    }
    options {
        ansiColor('xterm')    // Add's color to the output : Ensure you install AnsiColor Plugin.
    }
    stages{
        stage('Terraform Destroy Databases'){
            steps{
                git branch: 'main', url: 'https://github.com/23-Pravallika/terraform-dbs.git'
                    sh "terrafile -f ${ENV}-env/Terrafile"
                    sh "terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars"
                    sh "terraform plan -var-file=${ENV}-env/${ENV}.tfvars"
                    sh "terraform destroy -var-file=${ENV}-env/${ENV}.tfvars -auto-approve"
            }
        }
        stage('Terraform Destroy alb'){
            steps{
                git(branch: 'main', url: ' https://github.com/23-Pravallika/tf-loadbalancers.git')
                    sh "terrafile -f ${ENV}-env/Terrafile"
                    sh "terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars"
                    sh "terraform plan -var-file=${ENV}-env/${ENV}.tfvars"
                    sh "terraform destroy -var-file=${ENV}-env/${ENV}.tfvars -auto-approve"
            }
        }
        stage('Terraform Destroy Network'){
            steps{
                git branch: 'main', url: 'https://github.com/23-Pravallika/tf-vpc.git'
                    sh "terrafile -f ${ENV}-env/Terrafile"
                    sh "terraform init -reconfigure -backend-config=${ENV}-env/${ENV}-backend.tfvars"
                    sh "terraform plan -var-file=${ENV}-env/${ENV}.tfvars"
                    sh "terraform destroy -var-file=${ENV}-env/${ENV}.tfvars -auto-approve"
            }
        }
    }
}


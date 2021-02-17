pipeline {
    agent any
    tools {
        terraform 'terraform'
        }
    stages {
     stage('Git Checkout') {
            steps {
                git branch: 'devops', credentialsId: 'git', url: 'https://github.com/gauravk29/full_vpc'
            }
        } 
        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
            
        }
        stage('Terraform Plan') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                {
                sh 'terraform plan'
                }
            }
            }
        stage('Terraform Apply') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                {
                sh 'terraform apply --auto-approve'
                }
            }
        }
        stage('Terraform Destroy') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                {
                
                sh 'terraform destroy --auto-approve'
                }
            }
        }
    }
}


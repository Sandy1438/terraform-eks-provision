String credentialsId = 'AWS_4_TERRAFORM'

pipeline{

    agent any

    parameters {
	    choice(name: 'action', choices: 'create\ndestroy', description: 'Create/destroy of the deployment')
        }
    
    stages{
        stage("Terraform Initialization"){
            when {
                expression { params.action == 'create' }
            }
            steps{
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', 
                accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                credentialsId: 'AWS_4_TERRAFORM', 
                secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                        sh 'terraform init'
                }
            }
        }

        stage("Terraform plan"){
            when {
                expression { params.action == 'create' }
            }
            steps{
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', 
                accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                credentialsId: 'AWS_4_TERRAFORM', 
                secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    sh 'terraform plan'
                }
            }
        }

        stage("Terraform apply"){
            when {
                expression { params.action == 'create' }
            }
            steps{
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', 
                accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                credentialsId: 'AWS_4_TERRAFORM', 
                secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {               
                   sh 'terraform apply -auto-approve'
                }
            }
        }

        stage("Terraform destory"){
            when {
                expression { params.action == 'destroy' }
            }
            steps{
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', 
                accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                credentialsId: 'AWS_4_TERRAFORM', 
                secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {               
                   sh 'terraform destroy -auto-approve'
                }
            }
        }    
        
    }
}
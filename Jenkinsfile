pipeline {
     parameters {
       booleanParam(name: 'autoapprover', defaultValue: false, description: 'Automatically run apply after genrating plan' )
     }
     environment {
         AWS_ACCESS_KEY_ID  = credentials('AWS_ACCESS_KEY_ID')
         AWS_SECRET_ACCESS_KEY  = credentials('AWS_SECRET_ACCESS_KEY')
     }
  
    agent any
    stages {
        stage('Checkout') {
            steps {
                script{
                       dir("terraform")
                       {
                          git "https://github.com/gituser1305/docker1305/createEC2instanc.git"
                       }

                }
               
            }
        }

        stage('Terraform Init') {
            steps {
                script {
                    // Initialize Terraform
                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                script {
                    // Create a Terraform plan
                    sh 'terraform plan -out=tfplan'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                script {
                    // Apply the Terraform plan to create the EC2 instance
                    sh 'terraform apply -auto-approve tfplan'
                }
            }
        }

        stage('Terraform Destroy') {
            steps {
                script {
                    // If needed, you can add a stage to destroy the resources
                    // sh 'terraform destroy -auto-approve'
                }
            }
        }
    }

    post {
        success {
            // Optionally, you can add post-build actions here
        }
    }
}

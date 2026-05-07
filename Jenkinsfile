pipeline {
     agent {
        docker {
            image 'hashicorp/terraform:latest'
            args '--entrypoint=""'
        }
    }


    stages {

        stage('Terraform Plan') {
            steps {

                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) 
                {
                dir('Terraform')
                    {
                    sh 'terraform init'
                    sh 'terraform plan -out=tfplan'
                    sh 'terraform show tfplan > plan-output.txt'
                }
                }

                    post {
                            success {
                            archiveArtifacts artifacts: 'Terraform/plan-output.txt'
                            }
                        }

            }
        }

        stage('Approval'){
            steps{
                input 'Do you approve?'
            }
        }
    }
}
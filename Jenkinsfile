pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ca-central-1'
    }

    stages {

        stage('Terraform Plan') {
            steps {

                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
                    sh 'terraform init'
                    sh 'terraform plan -out=tfplan'
                    sh 'terraform show tfplan > plan-output.txt'
                }
            }
        }
    }
}
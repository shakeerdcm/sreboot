pipeline {
    agent  any
        options {
                timestamps ()
            }
    environment {
       CREDENTIALS_ID = 'sreboot'
  }

    stages {
        stage('checkout') {
            steps {
                 script{
                        dir("terraform")
                        {
                            git "https://github.com/shakeerdcm/sreboot.git"
                        }
                    }
                }
            }
    stage('Plan') {
            steps {
                sh 'pwd;cd TERRAFORM/GCEinstance ; terraform init -input=false'
                sh 'pwd;cd TERRAFORM/GCEinstance ; terraform workspace new ${environment}'
                sh 'pwd;cd TERRAFORM/GCEinstance ; terraform workspace select ${environment}'
                sh "pwd;cd TERRAFORM/GCEinstance ;terraform plan -input=false -out tfplan "
                sh 'pwd;cd TERRAFORM/GCEinstance ;terraform show -no-color tfplan > tfplan.txt'
            }
        }
    stage('Apply') {
            steps {
                sh "pwd;cd TERRAFORM/GCEinstance ; terraform apply -input=false tfplan"
            }
        }
    }
}

pipeline{
       agent any
      environment {
        TERRAFORM_INIT = "${fileExists('terraform_init') ? 'true' : 'false'}"
    }
    	parameters {
	     choice(
               name: 'ENV', 
               choices: ['dev1', 'dev2', 'stage','prod'], 
               description: 'Choose an Environment'
              )
	}
    
    stages{
	     stage('Debug Info') {
            steps {
                script {
                    echo "TERRAFORM_INIT: ${env.TERRAFORM_INIT}"
                    echo "Files in workspace:"
                    bat 'ls'
                }
            }
        }
      stage('AWS Deploy') 
      {
			steps 
            {
			    withCredentials([
                    aws(credentialsId: 'aws_cred')])
                      {
                        bat 'make --version'
                        //bat 'make tf-infra-init env='+ params.ENV
                      }
			}
      }
         stage('Terraform Setup') {
            steps {
                script {
                    if (env.TERRAFORM_INIT == 'false') {
                        // Run Terraform setup only in the first build
			     echo 'Terraform init'
                       // bat 'terraform init'
                       // bat 'terraform apply -auto-approve'

                        // Set the flag to indicate that Terraform setup has been completed
                        env.TERRAFORM_INIT = 'true'
                    } else {
                        echo 'Terraform setup has already been completed. Skipping.'
                    }
                }
            }
        
    }
}
}

pipeline{
       agent anyc
        environment {
        TERRAFORM_SETUP_COMPLETED = 'false'
        }
    	parameters {
	     choice(
               name: 'ENV', 
               choices: ['dev1', 'dev2', 'stage','prod'], 
               description: 'Choose an Environment'
              )
	}
    
    stages{
      stage('AWS Deploy') 
      {
			steps 
            {
			    withCredentials([
                    aws(credentialsId: 'aws_cred')])
                      {
                        //bat 'make --version'
                        bat 'make tf-infra-init env='+ params.ENV
                      }
			}
      }
         stage('Terraform Setup') {
            steps {
                script {
                    if (env.TERRAFORM_SETUP_COMPLETED == 'false') {
                        // Run Terraform setup only in the first build
                        sh 'terraform init'
                        sh 'terraform apply -auto-approve'

                        // Set the flag to indicate that Terraform setup has been completed
                        env.TERRAFORM_SETUP_COMPLETED = 'true'
                    } else {
                        echo 'Terraform setup has already been completed. Skipping.'
                    }
                }
            }
        
    }
}

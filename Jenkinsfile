pipeline{
       agent any
        environment {
        TERRAFORM_SETUP_COMPLETED_FILE = 'terraform_setup_completed'
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
                    def terraformSetupCompleted = fileExists(TERRAFORM_SETUP_COMPLETED_FILE)

                    if (!terraformSetupCompleted) 
                    {
                      withCredentials([
                      aws(credentialsId: 'aws_cred')])
                      {
                        //bat 'make --version'
                        //bat 'make tf-infra-init env='+ params.ENV
                      
                        // Run Terraform setup only in the first build
			            echo 'Terraform Init'
                     

                        // Create a file to indicate that Terraform setup has been completed
                        writeFile file: TERRAFORM_SETUP_COMPLETED_FILE, text: ''
                    } 
                    else {
                        echo 'Terraform setup has already been completed. Skipping.'
                    }
                }
			
			}
      }
   }
}

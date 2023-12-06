pipeline{
       agent any

    environment 
      {
        TERRAFORM_SETUP_COMPLETED_FILE2 = 'terraform_setup_completed2'
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
		    script {
                    def terraformSetupCompleted2 = fileExists(TERRAFORM_SETUP_COMPLETED_FILE2)

                    if (!terraformSetupCompleted2) 
                    {
                        //bat 'make --version'
                        //bat 'make tf-infra-init env='+ params.ENV
                      
                        // Run Terraform setup only in the first build
			            echo 'Terraform Init'
                     

                        // Create a file to indicate that Terraform setup has been completed
                        writeFile file: TERRAFORM_SETUP_COMPLETED_FILE2, text: ''
		            }
                    else {
                        echo 'Terraform setup has already been completed. Skipping.'
                    }
                }
	    }
			
			}
      }
   }

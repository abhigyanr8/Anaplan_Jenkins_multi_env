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
	    stage('Terraform Setup') {
            steps {
                script {
                    // Check if the file exists
                    def terraformSetupCompleted = fileExists(TERRAFORM_SETUP_COMPLETED_FILE)

                    if (!terraformSetupCompleted) {
                        // Run Terraform setup only in the first build
                        sh 'terraform init'
                        sh 'terraform apply -auto-approve'

                        // Create a file to indicate that Terraform setup has been completed
                        writeFile file: TERRAFORM_SETUP_COMPLETED_FILE, text: ''
                    } else {
                        echo 'Terraform setup has already been completed. Skipping.'
                    }
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
    //      stage('Terraform Setup') {
    //         steps {
    //             script {
    //                 if (env.TERRAFORM_INIT == 'false') {
    //                     // Run Terraform setup only in the first build
			 //     echo 'Terraform init'
    //                    // bat 'terraform init'
    //                    // bat 'terraform apply -auto-approve'

    //                     // Set the flag to indicate that Terraform setup has been completed
    //                     env.TERRAFORM_INIT = 'true'
    //                 } else {
    //                     echo 'Terraform setup has already been completed. Skipping.'
    //                 }
    //             }
    //         }
        
    // }
}
}

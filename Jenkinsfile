pipeline{
       agent any
    	parameters {
	     choice(
               name: 'ENV', 
               choices: ['dev1', 'dev2', 'stage','prod'], 
               description: 'Choose an Environment'
              )
	}
    
    stages{
      stage('AWS Deploy') {
			steps {
                                // bat 'echo' params.ENV
                                bat 'make --version'
                                bat 'make tf-infra-init env='+ params.ENV


                  }
            }
    }
}
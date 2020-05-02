pipeline {
    agent any
    parameters {
        choice(
            choices: ['develop' , 'release'],
            description: '',
            name: 'REQUESTED_ACTION')
    }
REQUESTED_ACTION = env.BRANCH_NAME;
    stages {
        stage ('clone') {
 	    
            when {
                // Only say hello if a "greeting" is requested
                expression { params.REQUESTED_ACTION == 'develop' }
            }
            steps {
                echo "Hello, Develop"
		
            }
	    /**when {
                // Only say hello if a "greeting" is requested
                expression { params.REQUESTED_ACTION == 'release' }
            }
            steps {
                echo "Hello, release"
		
            }**/
        }
    }
}

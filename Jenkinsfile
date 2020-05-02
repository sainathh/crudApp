pipeline {
    agent any
    parameters {
        choice(
            choices: ['develop' , 'release'],
            description: '',
            name: 'REQUESTED_ACTION')
    }

    stages {
        stage ('clone') {
	    echo "${env.BRANCH_NAME}"
 	    REQUESTED_ACTION = env.BRANCH_NAME;
            when {
                // Only say hello if a "greeting" is requested
                expression { params.REQUESTED_ACTION == 'develop' }
            }
            steps {
                echo "Hello, Develop"
		
            }
	    when {
                // Only say hello if a "greeting" is requested
                expression { params.REQUESTED_ACTION == 'release' }
            }
            steps {
                echo "Hello, release"
		
            }
        }
    }
}

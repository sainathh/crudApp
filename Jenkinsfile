node{
    echo "${workspace}"
    echo "${env.BRANCH_NAME}"
    echo "${env.TAG_NAME}"

    stage("clone"){
            git branch: env.BRANCH_NAME, url: '$github_url'
    }

    stage("build"){
        def mavenHome = tool name: "Maven363", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn "
        sh "${mavenCMD} clean package"
    }

    stage("deploy"){
	switch (env.BRANCH_NAME) {
		case develop:
		    println("Develop branch Build is completed\n Deploy to dev environment");
		    nexusArtifactUploader artifacts: [[artifactId: 'crudApp', classifier: '', file: 'target/crudApp.war', type: 'war']], credentialsId: 'NEXUS_CREDENTIALS', groupId: 'com.app', nexusUrl: '$nexus_url', nexusVersion: 'nexus3', protocol: 'http', repository: 'dev', version: '0.0.1-SNAPSHOT';
		    break;
		case release:
		    println("Release branch Build is completed\n Deploy to qa environment");
		    nexusArtifactUploader artifacts: [[artifactId: 'crudApp', classifier: '', file: 'target/crudApp.war', type: 'war']], credentialsId: 'NEXUS_CREDENTIALS', groupId: 'com.app', nexusUrl: '$nexus_url', nexusVersion: 'nexus3', protocol: 'http', repository: 'qa', version: '0.0.1-SNAPSHOT';
		    break;
        default:
            println("unknown");
            break;
    }
    }
}

node {
    stage("Clone"){
        git credentialsId: 'GIT_CREDENTIALS', url: 'https://github.com/sainathh/crudApp.git'
    }
    stage("build"){
        def mavenHome = tool name: "Maven363", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn "
		sh "${mavenCMD} clean package"
    }
    
}

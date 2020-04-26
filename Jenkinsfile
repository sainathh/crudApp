node {
    stage("Clone"){
        git credentialsId: 'GIT_CREDENTIALS', url: 'https://github.com/sainathh/crudApp.git'
    }
    stage("build"){
        def mavenHome = tool name: "MAVEN_3.6.3", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn "
		sh "${mavenCMD} clean package"
    }
    stage("deploy"){
        nexusArtifactUploader artifacts: [[artifactId: 'crudApp', classifier: '', file: 'target/**.war', type: 'war']], credentialsId: 'NEXUS_CREDENTIALS', groupId: 'com.app', nexusUrl: '54.175.171.187:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'test-1', version: '0.0.1-SNAPSHOT'
    }
}

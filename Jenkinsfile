node{
    
    stage("clone"){
            git branch: env.BRANCH_NAME, url: '$github_url'
    }
     stage("build"){
        def mavenHome = tool name: "Maven363", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn "
        sh "${mavenCMD} clean package"
    }
    stage("deploy"){
        def pom = readMavenPom file: 'pom.xml'
        if (env.BRANCH_NAME == "develop")
            nexusArtifactUploader artifacts: [[artifactId: 'crudApp', classifier: '', file: 'target/crudApp.war', type: 'war']], credentialsId: 'NEXUS_CREDENTIALS', groupId: 'com.app', nexusUrl: '$nexus_url', nexusVersion: 'nexus3', protocol: 'http', repository: 'dev', version: '0.0.1-SNAPSHOT'
        else if (env.BRANCH_NAME == "release")
            nexusArtifactUploader artifacts: [[artifactId: pom.artifactId, classifier: '', file: 'target/crudApp.war', type: pom.packaging]], credentialsId: 'NEXUS_CREDENTIALS', groupId: pom.groupId, nexusUrl: '$nexus_url', nexusVersion: 'nexus3', protocol: 'http', repository: 'qa', version: pom.version
        else if (env.BRANCH_NAME == "master")
            nexusArtifactUploader artifacts: [[artifactId: 'crudApp', classifier: '', file: 'target/crudApp.war', type: 'war']], credentialsId: 'NEXUS_CREDENTIALS', groupId: 'com.app', nexusUrl: '$nexus_url', nexusVersion: 'nexus3', protocol: 'http', repository: 'stage', version: '0.0.1-SNAPSHOT'
        else
            nexusArtifactUploader artifacts: [[artifactId: 'crudApp', classifier: '', file: 'target/crudApp.war', type: 'war']], credentialsId: 'NEXUS_CREDENTIALS', groupId: 'com.app', nexusUrl: '$nexus_url', nexusVersion: 'nexus3', protocol: 'http', repository: 'prod', version: '0.0.1-SNAPSHOT'
    }
}

node{
    sh "pwd"
    sh "r=`pwd`"
    sh "echo r"
    stage("clone"){
        git branch: 'develop', url: 'https://github.com/sainathh/crudApp.git'
    }
     stage("build"){
        def mavenHome = tool name: "Maven363", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn "
        sh "${mavenCMD} clean package"
    }
    stage("deploy"){
        nexusArtifactUploader artifacts: [[artifactId: 'crudApp', classifier: '', file: 'target/crudApp.war', type: 'war']], credentialsId: 'NEXUS_CREDENTIALS', groupId: 'com.app', nexusUrl: '18.207.203.164:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'test-1', version: '0.0.1-SNAPSHOT'
    }
}

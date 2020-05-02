def branch = env.BRANCH_NAME;
node{
    echo "${workspace}"
    echo "${env.BRANCH_NAME}"
    //GIT_BRANCH = sh(returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
    
    stage("clone"){
        
        git branch: 'env.BRANCH_NAME', url: 'https://github.com/sainathh/crudApp.git'       
       /** sh '''
            if [ $r -eq /var/lib/jenkins/workspace/multi_release ]
            then
                git branch: 'release', url: 'https://github.com/sainathh/crudApp.git'
            fi
        '''**/
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

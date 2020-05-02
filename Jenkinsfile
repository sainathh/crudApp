node{
    sh '''
        pwd
        r=`pwd`
        echo "branch: $r"
    '''
    stage("clone"){
        sh '''
            pwd
            r=`pwd`
            echo "branch: $r"
            echo "branch: ${r}"
            if [ $r -eq "/var/lib/jenkins/workspace/multi_develop" ]
            then
                git branch: 'develop', url: 'https://github.com/sainathh/crudApp.git'
            fi
        '''
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

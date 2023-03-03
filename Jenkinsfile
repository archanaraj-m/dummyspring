node('SPC_MAVEN')
{
    stage('vcs') { 
        git url:'https://github.com/archanaraj-m/dummyspring.git',
            branch: 'scripted'
    }
    stage ('build') {
        sh 'export PATH="/usr/lib/jvm/java-1.17.0-openjdk-amd64/bin:$PATH" && mvn package'
    }
    stage('postbuild') {
        archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                         onlyIfSuccessful: true
        junit testResults: '**/TEST-*.xml'
    }
}
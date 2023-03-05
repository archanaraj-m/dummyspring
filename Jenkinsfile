node('SPC_MAVEN')
{
    stage('vcs') { 
        git url:'https://github.com/archanaraj-m/dummyspring.git',
            branch: 'scripted'
    }
    stage('package') {
            tools {
                jdk 'JDK_17_UBUNTU'
                maven 'MAVEN_3.9.0_UBUNTU'
            } 
         steps{
            sh 'mvn package'
         }                       
    }
    stage('postbuild') {
        archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                         onlyIfSuccessful: true
        junit testResults: '**/TEST-*.xml'
    }
}
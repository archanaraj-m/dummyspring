node('SPC_MAVEN')
{
    stage('vcs') { 
        git url:'https://github.com/archanaraj-m/dummyspring.git',
            branch: 'scripted'
    }
    stage('package') {
        sh 'export PATH=/usr/lib/jvm/java-1.17.0-openjdk-amd64/bin:$PATH'
           'export MAVEN_HOME=/opt/maven'
           'export PATH=$PATH:$MAVEN_HOME/bin'
        sh 'mvn package' 
        }                       
    stage('postbuild') {
        archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                         onlyIfSuccessful: true
        junit testResults: '**/TEST-*.xml'
    }
}
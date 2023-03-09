pipeline {
    agent { label 'bucket' }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/archanaraj-m/dummyspring.git',
                    branch: 'bucket'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK_17_UBUNTU'
            }
            steps {
                sh "./mvnw ${params.MAVEN_GOAL}"
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/*.xml'
            }
        }        
        stage('copy to s3 bucket') {
            steps {
                sh "mkdir -p /tmp/${JOB_NAME}/${BUILD_ID}"
                sh "cp -r **/spring-petclinic-3.0.0-SNAPSHOT.jar /tmp/${JOB_NAME}/${BUILD_ID}"
                sh "aws s3 sync /tmp/${sonar-spc-declarative}/${BUILD_ID} s3://archanarajbucket9"
            }
        }
    }
}    
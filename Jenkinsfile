pipeline {
    agent { label 'java-app' }
    triggers { pollSCM ('H/30 * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/sekharc1230/spring-petclinic.git',
                branch: 'main'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK_8'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('postbuild') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                               onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'               
            }
        }
    }
}
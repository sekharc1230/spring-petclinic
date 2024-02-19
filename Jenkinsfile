pipeline {
    agent { label 'java-app' }
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
                sh 'mvn package'
            }
        }
    }
}
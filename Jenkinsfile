pipeline {
    agent { label 'LABEL4' }
    triggers { pollSCM ('* * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/msteja143/openmrs-core.git',
                    branch: 'master'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK-17'
            }
            steps {
                sh "mvn package"
            }
        }
        stage('post build') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}
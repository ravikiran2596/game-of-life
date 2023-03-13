pipeline {
    agent { label 'dockeragent'}
    triggers { pollSCM('* * * * *') }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/ravikiran2596/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('build goal') {
            tools {
                jdk 'jdk_8'
            }
            steps {
                sh "mvn ${params.maven_goal}"
            }
        }
        stage('archiveartifacts') {
            steps {
                archiveArtifacts onlyIfSuccessful: true,
                                 artifacts: '**/target/gameoflife.war'
            }
        }
        stage('junittest') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml',
                allowEmptyResults: true
            }
        }
    }
}
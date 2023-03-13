pipeline {
    agent { label 'dockeragent'}
    triggers { pollSCM('* * * * *') }
    parameters { choice(name: 'maven_goal', choices: ['package', 'install', 'clean'], description: 'maven goal') }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/ravikiran2596/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('build') {
            tools {
                jdk 'jdk_8'
            }
            steps {
                sh 'mvn package'
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
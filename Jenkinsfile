pipeline {
    agent { label 'dockeragent'}
    stages ('vsc') {
        steps {
            git 'https://github.com/ravikiran2596/game-of-life.git'
        }
    }
    stages ('build') {
        steps {
            build 'mvn package'
        }
    }
    stages ('test') {
        steps {
            junit '**/surefire-reports/TEST-*.xml'

        }
    }
    stages ('artifactory') {
        steps {
            archiveArtifacts artifacts: '**/target/gameoflife.war'
        }
    }
}
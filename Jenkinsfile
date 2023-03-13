pipeline {
    agent { label 'dockeragent'}
    stages('vsc') {
        steps {
            git url: 'https://github.com/ravikiran2596/game-of-life.git'
               branch: 'master'
        }
    }
    stages('build') {
        steps {
            sh 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && mvn package'
        }
    }
    stages('artifactory') {
        steps {
            archiveArtifacts artifacts: '**/target/gameoflife.war'
        }
    }       
    stages('test') {
        steps {
            junit '**/surefire-reports/TEST-*.xml'

        }
    }
}
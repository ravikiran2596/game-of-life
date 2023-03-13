node ('dockeragent') {
    stage('vcs') {
        git url: 'https://github.com/ravikiran2596/game-of-life.git',
            branch: 'master'
    }
    stage('build') {
        sh 'export="/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH" && mvn package'
    }
    stage(archiveArtifacts) {
        archiveArtifacts onlyIfSuccessful: true,
        artifacts: '**/target/gameoflife.war',
        allowEmptyArchive: false
    }
    stage('testresult') {
        junit testResults: '**/surefire-reports/TEST-*.xml',
        allowEmptyResults: true
    }
}
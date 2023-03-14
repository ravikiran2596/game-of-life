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
        stage('build') {
            tools {
                jdk 'jdk_8'
            }
            steps {
                sh "mvn package"
            }
        }
        stage('sonar analysis') {
            steps {
                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('sonar_cloud') {
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=gameoflife1'
                }
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
    post {
        success {
            mail subject: "jenkins build of &${JOB_NAME} with id ${BUILD_ID} is success",
                 body: "use this URL ${BUILD_URL} for more info",
                 to: 'foo@acme.org',
                 from: 'foo@abc.org'
        } 
        failure {
            mail subject: "jenkins build of &${JOB_NAME} with id ${BUILD_ID} is success",
                 body: "use this URL ${BUILD_URL} for more info",
                 to: "${GIT_AUTHOR_EMAIL}",
                 from: 'foo@abc.org'
        }
    }
}
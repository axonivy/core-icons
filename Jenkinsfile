pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11'
    }
  }

  options {
    buildDiscarder(logRotator(artifactNumToKeepStr: '20'))
  }

  triggers {
    cron '@midnight'
  }

  stages {    
    stage('build') {
      steps {
        script {
          maven cmd: "clean deploy"
        }
        archiveArtifacts 'target/*.jar'
        recordIssues tools: [mavenConsole()], unstableTotalAll: 1
      }
    }
  }
}

pipeline {
  agent {
    docker {
      image 'maven:3.8.6-eclipse-temurin-17'
    }
  }

  options {
    buildDiscarder(logRotator(numToKeepStr: '20', artifactNumToKeepStr: '2'))
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
        recordIssues tools: [mavenConsole()], qualityGates: [[threshold: 1, type: 'TOTAL']]
      }
    }
  }
}

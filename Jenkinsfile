#!/bin/env groovy

pipeline {

  agent none


  stages {
    stage('Init') {
      agent {
        dockerfile {
          dir '.jenkins'
          filename 'Dockerfile-init'
        }
      }
      steps {
        script {
          env.GIT_BRANCH_NAME = sh (script: 'git name-rev --name-only HEAD', returnStdout: true).trim().minus(~/^remotes\/origin\//)
          env.IS_SNAPSHOT = getMavenVersion().endsWith("-SNAPSHOT")
          env.MAVEN_CONFIG = " -Dform-dist-repo.snapshots.url=${params.MAVEN_SNAPSHOTS_REPO}"
        }
      }
    }
  }
}
}

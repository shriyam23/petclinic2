pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Starting build'
        sh 'mvn clean install -e -Dlicense.skip=true -Dserver.port=8888'
        echo 'Build step complete'
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts 'target/*'
      }
    }

  }
}

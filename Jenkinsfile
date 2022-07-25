pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Starting build'
        sh 'mvn clean install -Dlicense.skip=true -Dserver.port=8888'
      }
    }

  }
}
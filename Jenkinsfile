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

    stage('Testing') {
      steps {
        sh '''mvn clean verify sonar:sonar -Dsonar.projectKey=petclininc -Dsonar.host.url=https://34.237.162.141:9000 -Dsonar.login=3a1f24d74b59c66cb66bf95696f005674cb37cd -Dsonar.sources=sr -Dlicense.skip=true -Dserver.port=8888
'''
      }
    }

  }
}
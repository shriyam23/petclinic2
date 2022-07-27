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
        withSonarQubeEnv('sonarqubelocal') {
          sh '''mvn install org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar
                mvn verify sonar:sonar \\
                -Dsonar.host.url=http://44.209.210.127:9000 \\
                -Dsonar.login=ee1766939251f12d38a6287607cb75939b5157dd\\
                -Dsonar.sources=src/main/java\\
                -Dlicense.skip=true\\
                -Dsonar.java.binaries=target/classes\\
'''
        }

      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts 'target/*'
      }
    }

    stage('Execute') {
      steps {
        sh 'java -Dserver.port=8888 -jar target/*.jar'
      }
    }

  }
}
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
                -Dsonar.host.url=http://3.225.167.125:9000 \\
                -Dsonar.login=e5d2929e2d8605d8d7594dc83fa8bd45cd973dd1\\
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
        sh '''kill -9 $(lsof -i:8888 -t) 2> /dev/null
java -Dserver.port=8888 -jar target/*.jar&'''
      }
    }

  }
}
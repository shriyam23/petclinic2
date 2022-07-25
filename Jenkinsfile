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
          sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar'
        }

        sh '''mvn clean package sonar:sonar
mvn clean verify sonar:sonar \\
-Dsonar.host.url=http://3.225.167.125:9000 \\
-Dsonar.login=e5d2929e2d8605d8d7594dc83fa8bd45cd973dd1\\
-Dsonar.sources=src\\
-Dlicense.skip=true\\
-Dsonar.exclusions=**/*.java'''
      }
    }

  }
}
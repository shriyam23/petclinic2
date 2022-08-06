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

    stage('SCM Checkout') {
      steps {
        git(url: 'https://github.com/shriyam23/petclinic2.git', branch: 'main', poll: true)
      }
    }

    stage('Deploy') {
      steps {
        ansiblePlaybook(playbook: 'deployment.yml', becomeUser: 'root', disableHostKeyChecking: true, credentialsId: 'private-key', sudoUser: 'root', inventory: 'inventory')
      }
    }

  }
}
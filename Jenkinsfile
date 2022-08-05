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

    stage('Deployment') {
      steps {
        ansiblePlaybook(playbook: 'deployment.yml', credentialsId: 'private-key', installation: 'Ansible', inventory: 'dev.inv', becomeUser: 'root', forks: -100, sudoUser: 'root', disableHostKeyChecking: true)
      }
    }

  }
}
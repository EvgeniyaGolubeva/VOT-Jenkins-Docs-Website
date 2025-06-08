pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        git 'https://github.com/EvgeniyaGolubeva/VOT-Jenkins-Docs-Website.git'
      }
    }
    stage('Build') {
      steps {
        echo 'Nothing to build for static site'
      }
    }
    stage('Deploy') {
      steps {
        sh 'sudo cp -r * /var/www/html/'
      }
    }
  }
}

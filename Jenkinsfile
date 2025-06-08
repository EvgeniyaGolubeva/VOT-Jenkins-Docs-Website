pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        git branch: 'main', url: 'https://github.com/EvgeniyaGolubeva/VOT-Jenkins-Docs-Website.git'
      }
    }
    stage('Build') {
      steps {
        echo 'Nothing to build for static site'
      }
    }
    stage('Deploy') {
      steps {
        sh 'sudo cp -r Jenkinsfile index.html style.css /var/www/html/'
      }
    }
  }
}

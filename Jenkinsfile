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
    stage('Docker Build') {
    steps {
        sh '''
        docker build -t my-docs-site .
        docker stop docs-container || true
        docker rm docs-container || true
        docker run -d --name docs-container -p 8081:80 my-docs-site
        '''
    }
    }
    stage('Deploy') {
    steps {
        sh '''
        sudo mkdir -p /var/www/html
        sudo cp -r Jenkinsfile index.html style.css /var/www/html/
        '''
    }
    }
  }
}




pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/ddriham/hello-world-python/tree/master', branch: 'master')
      }
    }

    stage('build') {
      steps {
        sh 'docker build -t hello-world-python:$BUILD_NUMBER .'
      }
    }

    stage('test') {
      steps {
        sh 'docker run -itd --name hello-world-python -p 8080:8080 hello-world-python:$BUILD_NUMBER'
        sleep 5
        sh 'curl localhost:8080'
        sh 'docker stop hello-world-python && docker rm hello-world-python'
      }
    }

    stage('push to dockerhub') {
      steps {
        sh 'docker login'
        sh 'docker push hello-world-python:$BUILD_NUMBER'
      }
    }

  }
}
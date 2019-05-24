pipeline {
  agent any
  stages {
    stage('test') {
      steps {
        echo 'test'
      }
    }
    stage('test2') {
      steps {
        sleep 4
      }
    }
    stage('test3') {
      steps {
        error 'test'
      }
    }
  }
}
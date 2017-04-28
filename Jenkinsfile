pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        git 'https://github.com/mrdriller/jenkins_example.git'
        sh 'CMake .'
        sh 'make'
      }
    }
  }
}
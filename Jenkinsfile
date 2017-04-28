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
    stage('Unit tests') {
      steps {
        parallel(
          "Unit tests": {
            sh '''
make unit_tests'''
            
          },
          "Integration tests": {
            sh 'make integration_tests'
            
          },
          "GUI tests": {
            sh 'make gui_tests'
            
          }
        )
      }
    }
    stage('Documentation') {
      steps {
        sh 'make docs'
      }
    }
    stage('cpplint') {
      steps {
        parallel(
          "cpplint": {
            sh 'cpplint.py *.cpp 2> cpplint_warnings.txt || true'
            
          },
          "cppcheck": {
            sh 'cppcheck --enable=warning --enable=portability --enable=style src 2> cppcheck-result.xml'
            
          }
        )
      }
    }
    stage('Publish test results') {
      steps {
        junit 'testing/unit_test_detail.xml,testing/integration_test_detail.xml'
      }
    }
  }
}
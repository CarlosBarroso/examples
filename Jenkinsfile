def BUILD_NUMBER
BUILD_NUMBER=env.BUILD_NUMBER

pipeline {
  agent any
  stages {
    stage('step 1') {
      steps {
        println 'this branch is the build '
        println BUILD_NUMBER
        println DEMO
      }
    }
  }
  environment {
    DEMO = '1'
  }
}
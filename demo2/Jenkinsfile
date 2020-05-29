def _BUILD_NUMBER
_BUILD_NUMBER=env.BUILD_NUMBER

pipeline {
  agent any
  stages {
    stage('step 1') {
      steps {
        echo "this is the build $BUILD_NUMBER"
        sh '''
          echo "using a multi-lien shell step"
          chmod +x test.sh
          ./test.sh
        '''
      }
    }

  }
  environment {
    DEMO= "beta"
  }
}
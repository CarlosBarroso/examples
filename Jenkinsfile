def _BUILD_NUMBER
_BUILD_NUMBER=env.BUILD_NUMBER

def notify(status){
    emailext (
      to: "you@gmail.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}

pipeline {
  agent {
    docker {
      image 'mcr.microsoft.com/docnet/core/sdk:3.1.101'
    }
  }
  stages {
    stage('verify') {
      steps {
        sh ''' 
          dotnet --list-sdks
          dotnet --list-runtimes
        '''
        sh 'printenv'
        sh 'ls -l "$WORKSPACE"'
      }
    }    
    stage('step 1') {
      steps {
        echo "Send start email"
        notify('Started')

        echo "this is the build $BUILD_NUMBER"
        sh '''
          echo "using a multi-lien shell step"
          chmod +x test.sh
          ./test.sh
        '''
      }
    }
    stage('step 2') {
      steps {
        writeFile file: "resultados.txt", text: "passed $BUILD_NUMBER" 
        script {
          if (Math.random() > 0.9) {
            throw new Exception()
          }
        }
      }
    }

  }
  post {
    success {
      archiveArtifacts 'resultados.txt'
      notify 'Success'

    }
    failure {
      notify 'fail'
    }
  } 

  environment {
    DEMO = '1'
  }
}
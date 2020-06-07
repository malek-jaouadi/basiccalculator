pipeline {
  agent { docker 
         { 
           image 'python:3.6.9'
           args '-u root:sudo'
         } }
  stages {
    stage('build') {
      steps {
        sh '''
        pip install -r requirements.txt
        '''
      }
      }
  }
}

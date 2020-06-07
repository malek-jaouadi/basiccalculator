pipeline {
  agent { docker { image 'python:3.6.9' } }
  stages {
    stage('build') {
      steps {
        sh '''
        virtualenv venv
        source venv/bin/activate
        pip install -r requirements.txt
        '''
      }
      }
  }
}

pipeline {
  agent any
  stages {
         stage ('setup newman & system tests') {
             agent {
                  docker { 
                          image 'postman/newman_alpine33'
                         }}
          stages{
           stage('launch application') {
            steps {
              sh '''
                  yum install python3
                  python calculator.py &            
                  '''
              }}
            stage('Newman Tests') {
            steps {
              sh 'newman run tests/system/calculator.postman_collection.json'
              }}
              } 
        }}}

pipeline {
  agent any
  stages {
    stage('Tests') {
      agent 
      {
       docker 
         { 
           image 'python:3.6.9'
           args '-p 5000:5000 -u "$(id -u):$(id -g)" -v /etc/passwd:/etc/passwd:ro'
         } }
       stages{
         stage('install requirements')
         {
           steps {
             sh '''
             pip install -r requirements.txt
             '''
          }}
          stage('Unit test') {
            steps {
              sh 'python -m unittest'
              }   
              }
          stage('launch application') {
            steps {
              sh 'python calculator.py'
              }   
              }
          stage('system test') {
            steps {
              sh 'newman run tests/system/calculator.postman_collection.json'
              }   
              }
        }}
   
  }
}

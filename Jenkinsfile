pipeline {
  agent any
  stages {
    stage('Tests') {
      agent { 
        docker { 
           image 'malekdocker/python3.6.9_newman'
           args '-u root:sudo'
         } }
       stages{
         stage('install requirements') {
           steps {
             sh '''
             pip install -r requirements.txt
             '''
             }}
          stage('Unit test') {
            steps {
              sh 'pytest --junitxml tests/reports_unittest/results.xml tests/unit/'
              }}
          stage('launch application') {
            steps {
              sh 'python calculaator.py &'
              }}
          stage('Newman Tests') {
            steps {
              sh 'newman run tests/system/calculator.postman_collection.json'
              }}
       }}
         }}
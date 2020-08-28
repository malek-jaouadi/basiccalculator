pipeline {
  agent { 
        docker { 
           image 'python:3.6.9'
           args '-u root:sudo'
         } }
  stages {
    stage('Tests') {
       stages{
         stage('install requirements') {
           steps {
             sh '''
             pip install -r requirements.txt
             '''
             }}
          stage('Unit test') {
            steps {
              sh 'python -m unittest'
              }}
          stage('launch application') {
            steps {
              sh 'python calculator.py &'
              }}
       }}
         stage ('setup newman & system tests') {
             agent {
                  docker { 
                          image 'postman/newman_alpine33'
                         }}
            steps {
              sh 'Heelllooooooooooooo'
              }   
        }}}

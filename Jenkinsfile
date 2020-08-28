pipeline {
  agent any
  stages {
    stage('Tests') {
      agent { 
        docker { 
           image 'python:3.6.9'
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
              sh 'python -m unittest'
              }}
       }}
         stage ('setup newman & system tests') {
             agent {
                  docker { 
                          image 'postman/newman_alpine33'
                         }}
          stages{
           stage('launch application') {
            steps {
              sh 'python calculator.py &'
              }}
            stage('Newman Tests') {
            steps {
              sh 'newman run tests/system/calculator.postman_collection.json'
              }}
              } 
        }}}

pipeline {
  agent any
  options {
    timeout(time: 4, unit: 'MINUTES')
  }
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
              sh 'pytest --junitxml reports/results.xml tests/unit/'
              }
              post {
                    always {
                        junit 'reports/*.xml'
                        }}
              }
        stage('Code Quality Check via SonarQube') {
          agent {
            label 'master'
          }
          environment {
            TOKEN_SONAR = credentials('token_sonar_calculator')
              }
          steps {
            script {
              def scannerHome = tool 'sonnar_scanner';
              withSonarQubeEnv("SonarQube") {
                  sh "${tool("sonnar_scanner")}/bin/sonar-scanner \
                     -Dsonar.projectKey=calculator \
                     -Dsonar.sources=. \
                     -Dsonar.host.url=http://ec2-35-180-86-71.eu-west-3.compute.amazonaws.com:9000 \
                     -Dsonar.login=$TOKEN_SONAR"
                    }}
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
         }
         }
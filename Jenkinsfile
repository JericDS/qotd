pipeline {
  agent any
  
  stages {
  	stage('Compile') { 
      steps {
        sh 'mvn clean compile'
      }
    }
    stage('Unit Test') { 
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('5970cd6b-c817-49f2-9a1a-85a620d29f2f')
      }
      steps {
        sh 'mvn deploy -P cloudhub -Dmule.version=3.9.0 -Danypoint.username=${ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}' 
      }
    }
  }
}
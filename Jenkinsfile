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
        ANYPOINT_CREDENTIALS = credentials('6e796489-3775-488e-b67e-9264b4793cbb')
      }
      steps {
        sh 'mvn deploy -P cloudhub -Dmule.version=3.9.0 -Danypoint.username=${ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}' 
      }
    }
  }
}
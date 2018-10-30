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
    stage('Sonar Analysis') {
      steps {
        withSonarQubeEnv('Sonar Server') {
          sh 'mvn clean package sonar:sonar'
        }
      }
    }
    stage("Quality Gate") {
      steps {
        timeout(time: 1, unit: 'HOURS') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
    stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
      }
      steps {
        sh 'mvn deploy -P cloudhub -Dmule.version=3.9.0 -Danypoint.username=${ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}' 
      }
    }
  }
}
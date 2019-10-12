pipeline {
  agent any
  stages {
    stage('Unit Test') {
      steps {
        sh 'mvn clean test'
      }
    }
    stage('Deploy Standalone') {
      steps {
        sh 'mvn deploy -P standalone'
      }
    }
    stage('Deploy ARM') {
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials1')
      }
      steps {
        sh 'mvn deploy -P arm -Darm.target.name=local-3.8.3-ee -Danypoint.username=${anypoint.credentials1_USER} -Danypoint.password=${anypoint.credentials1_PSW}'
      }
    }
    stage('Deploy CloudHub') {
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials1')
      }
      steps {
        sh 'mvn deploy -P cloudhub -Dmule.version=3.8.3 -Danypoint.username=${anypoint.credentials1_USER} -Danypoint.password=${anypoint.credentials1_PSW}'
      }
    }
  }
}

pipeline {
  agent { label 'new-workstation'}

  stages {

    stage('Download Dependencies'){
      steps {
        sh 'npm install'
      }
    }

    stage('Code Quality') {
      steps {
        sh 'sonar-scanner -Dsonar.host.url=http://172.31.34.168:9000 -Dsonar.login=admin -Dsonar.password=admin1234 -Dsonar.projectKey=backend'
      }
    }

    stage('Unit Tests'){
      steps {
        //Ideally we should run tyhe tests, but here the developer have not used it.
        echo 'CI'
      }
    }

    stage('Release') {
      steps {
        echo 'CI'
      }
   }
 }
 
} /////
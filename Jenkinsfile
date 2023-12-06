pipeline {
  agent { label 'new-workstation'}

  stages {

    stage('Download Dependencies'){
      steps {
        sh 'npm install'
      }
    }

    stage('Code Quality') {
      when {
        allOf {
          branch 'main'
          expression { env.TAG_NAME !=~ env.BRANCH_NAME }
        }
      }
      steps {
        sh 'sonar-scanner -Dsonar.host.url=http://172.31.34.168:9000 -Dsonar.login=admin -Dsonar.password=admin1234 -Dsonar.projectKey=backend -Dsonar-qualitygate.wait=true'
      }
    }

    stage('Unit Tests'){
      when {
        allOf {
          branch 'main'
        }
      }
      steps {
        //Ideally we should run tyhe tests, but here the developer have not used it.
        echo 'CI'
      }
    }

    stage('Release') {
      when {
        expression { env.TAG_NAME ==~ ".*" }
        }
      steps {
        echo 'CI'
      }
   }
 }
 
} 
pipeline {
  agent { label 'new-workstation'}

  stages {

    stage('Download Dependencies'){
      steps {
        sh 'npm install'
        sh 'env'
      }
    }

    stage('Code Quality') {
      when {
        allOf {
          expression { env.TAG_NAME != env.BRANCH_NAME }
        }
      }
      steps {
        //sh 'sonar-scanner -Dsonar.host.url=http://172.31.34.168:9000 -Dsonar.login=admin -Dsonar.password=admin1234 -Dsonar.projectKey=backend -Dsonar-qualitygate.wait=true'
        echo 'OK'
      }
    }

    stage('Unit Tests'){
      when {
        allOf {
          expression { env.TAG_NAME != env.BRANCH_NAME }
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
        
      //steps {
      //  sh 'zip -r backend-${TAG_NAME}.zip node_modules schema DbConfig.js index.js package.json TransactionService.js'
      //  sh 'curl -sSf -u "admin:Dontknow29" -X PUT -T backend-${TAG_NAME}.zip "http://artifactory.vaishnavidevops.online:8081/artifactory/backend/backend-${TAG_NAME}.zip"'
      //}

      steps {
        sh 'docker build -t 851512651356.dkr.ecr.us-east-1.amazonaws.com/backend:${TAG_NAME} .'
        sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 851512651356.dkr.ecr.us-east-1.amazonaws.com'
        sh 'docker push 851512651356.dkr.ecr.us-east-1.amazonaws.com/backend:${TAG_NAME}'
      }
   }
 }
 
} 

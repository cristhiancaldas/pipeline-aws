 pipeline {
   agent any
    stages {

       stage ('Build') {
             steps {
                  sh './gradlew assemble'
             }
       }

       stage ('Test') {
             steps {
                  sh './gradlew test'
             }
       }

       stage('Deploy to AWS'){
             if (env.BRANCH_NAME == 'main') {
             steps{
                   withAWS(credentials: 'aws-acceskey', region: 'us-east-1') {
                      sh './gradlew awsCfnMigrateStack awsCfnWaitStackComplete'
                   }
             }
          }else {
             echo "${env.BRANCH_NAME}"
          }
       }
   }
 }
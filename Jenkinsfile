

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
             steps{
                   withAWS(credentials: 'aws-acceskey', region: 'us-east-1') {
                    script {
                       if (env.BRANCH_NAME == 'main') {
                          sh './gradlew awsCfnMigrateStack awsCfnWaitStackComplete'
                          }
                    }
                   }
            }
       }
   }
 }
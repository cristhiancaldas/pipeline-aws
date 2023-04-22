

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
                   withAWS(credentials: 'aws-acceskey', region: env.AWS_REGION) {
                          sh './gradlew awsCfnMigrateStack awsCfnWaitStackComplete'
                   }
            }
       }
   }
 }
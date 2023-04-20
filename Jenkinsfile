 pipeline {
   agent any
   tools {
        jdk   'JAVA_HOME'
   }
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

       stage('Deploy AWS'){
             steps{
                  script{
                        withAWS(credentials: 'aws-credentials', region: env.AWS_REGION) {
                                          sh './gradlew awsCfnMigrateStack awsCfnWaitStackComplete'
                        }
                  }
             }
       }
  }
 }
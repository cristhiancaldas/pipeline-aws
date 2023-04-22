

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
                    script {
                    echo env.BRANCH_NAME
                    echo "user: ${env.BRANCH_NAME}"
                       if (env.BRANCH_NAME == 'main') {
                          sh './gradlew awsCfnMigrateStack awsCfnWaitStackComplete'
                          }else {
                          echo 'No estas en la rama correcta'
                          }
                    }
                   }
            }
       }
   }
 }
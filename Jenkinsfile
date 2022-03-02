pipeline {
    agent any

    tools {
        maven "M3"
    }

    environment {
        DEV = "src/main/environments/dev"
        SIT = "src/main/environments/sit"
        UAT = "src/main/environments/uat"
        PROD = "src/main/environments/prod"
    }

    stages {
        stage ('Checkout Source Code') {
            steps {
                checkout scm
            }
        }

        stage('Prepare Environment') {
            steps {
                script {
                  withCredentials([usernamePassword(credentialsId: 'APIM_ADMIN_USERNAME_PASSWORD_DEV_ENV', usernameVariable: 'username', passwordVariable: 'password')]) {
                        env.APIM_ADMIN_USER=username
                        env.APIM_ADMIN_PASSWORD=password
                        env.AXWAY_APIM_CLI_HOME = DEV
                  }
                }
            }
        }

        stage('Build Package'){
            steps{
                sh "mvn clean install"
            }
        }

        stage('Deploy API'){
            steps{
                sh "mvn exec:java"
            }
        }

   }
}

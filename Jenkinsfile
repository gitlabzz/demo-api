pipeline {
   agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "Mvn 3.6.3"
   }

   stages {
      stage('Build') {
         steps {
            // Get the repository from GitHub
            git 'https://github.com/gitlabzz/demo-api.git'
            // Run Maven
            sh "mvn clean exec:java"

            sh 'mvn clean exec:java -Dexec.args="-h ${host} -u ${username} -p ${password} -c ./api-definition/1-design-only-config.json -s api-env -f true -returnCodeMapping 10:0"'

            // If you prefer to use Jenkins-Credentials instead of APIM_CLI_HOME/conf use this instruction
            /* withCredentials([usernamePassword(credentialsId: "${stage}", usernameVariable: 'username', passwordVariable: 'password')])  {
                sh 'mvn clean exec:java -Dexec.args="-h ${host} -u ${username} -p ${password} -c ./api-definition/1-design-only-config.json -s api-env -f true -returnCodeMapping 10:0"'
            } */                   }
      }
   }
}

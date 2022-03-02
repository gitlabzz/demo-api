node {

    def mvnHome

    stage('Checkout Code') {
        git branch: '${BRANCH_NAME}', credentialsId: '2bc605b8-3d32-4c7b-84e2-4d858bc31c46', url: 'https://github.com/gitlabzz/demo-api.git'
    }

    stage('Prepare Environment') {
        mvnHome = tool 'M3'
        withCredentials([usernamePassword(credentialsId: 'APIM_ADMIN_USERNAME_PASSWORD_DEV_ENV', passwordVariable: 'password', usernameVariable: 'username')]) {
            env.APIM_ADMIN_USER = username
            env.APIM_ADMIN_PASSWORD = password
            env.AXWAY_APIM_CLI_HOME = "src/main/environments/dev"
        }
    }

    stage('Publish API') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" exec:java'
            }
        }
    }

    stage('Prepare Package') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" clean install'
            }
        }
    }

    stage('Push Package to Nexus') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                // TODO: later make it deploy instead of install
                sh '"$MVN_HOME/bin/mvn" clean install'
            }
        }
    }
}
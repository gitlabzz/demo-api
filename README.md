## Dependency
cd /Users/dev/Development/github/AndriyKalashnykov/spring-on-k8s
mvn clean install spring-boot:run
http://172.16.63.1:8088/actuator
http://172.16.63.1:8088/swagger-ui/
http://172.16.63.1:8088/v2/api-docs?group=public-api


## PATH SETUP
export AXWAY_APIM_CLI_HOME=/Users/dev/Development/axway/apim-cli/distribution/target/axway-apimcli-1.10.0-SNAPSHOT/apim-cli-1.10.0-SNAPSHOT

-- check to confirm ---

export AXWAY_APIM_CLI_HOME=/Users/dev/Development/axway/bct/apim_cicd/demo-api/src/main/environments/dev (Yes, it works. As long as there is a conf folder with env specific properties file)
mvn clean exec:java

export SWAGGER_PROMOTE_HOME=$AXWAY_APIM_CLI_HOME
export PATH=$AXWAY_APIM_CLI_HOME/scripts:$PATH
cp /Users/dev/Development/axway/bct/apim_cicd/demo-api/src/main/environments/dev/env.dev.properties $AXWAY_APIM_CLI_HOME/conf

## RUN APIM-CLI FROM SHELL
ADD ~/Development/axway/tools/apim-cli-1.9.0/scripts to $PATH
cd /Users/dev/Development/axway/bct/apim_cicd/demo-api/src/main/resources
apim.sh api import -s dev -c api-config.json

or
apim.sh api import -a samples/petstore.json -c samples/minimal-config.json -h localhost -u apiadmin -p changeme -clientAppsMode ignore -ignoreQuotas true


or
export APIM_ADMIN_USER=apiadmin
export APIM_ADMIN_PASSWORD=changeme1
export AXWAY_APIM_CLI_HOME=src/main/environments/dev
mvn clean install exec:java

## RUN USING MAVEN
mvn clean exec:java


#### API GATEWAY MANAGER
https://172.16.63.128:8090/
admin/changeme

#### API MANAGER
https://172.16.63.128:8075/home
apiadmin/changeme1


#### VERIFY
https://172.16.63.128:8065/api/v2
http://172.16.63.128:8065/v2/api-docs?group=public-api
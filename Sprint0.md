
# Server

- ldng-config-server will be a Spring Boot application that will be a deployable WAR file
- For SVN, SVNKit licensing is required.
- Config files can be separated by application folders under the git/svn base uri. e.g. ldng-ts/ldng-ts.properties, ldng-ts/ldng-ts-development.properties

# Client

- bootstrap.yml has to specify the application.name, which should be the same as the config name (e.g ldng-es-web).
- To refresh the configuration from the Config Server, send a HTTP POST request to the /refresh endpoint. JMX can also be used to refresh the configuration.
- 

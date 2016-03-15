# Spring Config Server Prototype

The intent of the prototype is to implement an end-to-end Spring Config enabled Server and Client application in LDNG that stores the configuration in SVN and a configuration change to the  config file in SVN is reflected on the client application without restarts. The following components were developed/modified.

* A new Spring Config Server instance connected to SVN that provides the configuration for the LDNG ES application 
* The LDNG ES application modified to use Spring Boot that loads it's configuration from the Config Server on startup and refreshes the configuration on demand.    

# Server

- The Server code is available in SVN under http://plsysadm-cm07:8888/cm-repos/ldng/devbranches/LDNG.1.3_INT_DEV_CONFIGSRV/config-server
- config-server will be a Spring Boot application that will be a deployable WAR file, specified by the 'packaging' tag in pom.xml. To build a war file that is both executable and deployable into an external container embedded container dependencies are marked as 'provided'.
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <!-- ... -->
    <packaging>war</packaging>
    <!-- ... -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
        <!-- ... -->
    </dependencies>
</project>

```
- For SVN, SVNKit licensing is required. http://svnkit.com/licensing.html
- Config files can be separated by application folders under the svn base uri. e.g. ldng-ts/ldng-ts.properties, ldng-ts/ldng-ts-development.properties. The 'searchPaths' property in bootstrap.yml is used to specifiy the folders.
- The SVN folder structure has to use the SVN standard 'tags', 'branches' and 'trunk' strucuture. The config file folders should exisit under these SVN folders. In addition, for older Spring Config library versions, the 'master' folder is required. 

# Client

- The LDNG ES application was converted to a Spring Boot Application, which involves adding dependencies and additional configuration.
- bootstrap.yml has to specify the application.name, which should be the same as the config name (e.g ldng-es-web).
- To refresh the configuration from the Config Server, send a HTTP POST request to the /refresh endpoint. JMX can also be used to refresh the configuration.

## Changes 

- Spring Boot 1.2.1.RELEASE depends on Spring framework 4.1.4.RELEASE.
- Spring Boot Cloud on the client needs to be 1.0.0.RELEASE
- The following dependencies were added to pom.xml. A spring boot maven plugin is also required for packaging. 
 ```
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
			<version>1.2.1.RELEASE</version>
		</dependency>		
		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
			<scope>provided</scope>
			<version>1.2.1.RELEASE</version>
		</dependency>
		
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
			<version>1.2.1.RELEASE</version>
		</dependency>	
		
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-config-server</artifactId>
			<version>1.0.4.RELEASE</version>
		</dependency>
		.....
		<plugin>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-maven-plugin</artifactId>
		</plugin>

```
- 


# Server

- The Server is a Spring Boot app. The config source can be git, svn or filesystem.
- SVN support is provided, but the underlying repository implementation is provided through SNNKit and must be licensed (http://svnkit.com/licensing.html)
- Security: Many options through Spring Boot Security. In theory, the Config Server can be deployed as a regular WAR in FNMA standard TC server, secured with ESSO. 

# Client

- The Config Server is meant to be used by a Spring boot client. This is the "natural" way. REST endpoints can be used by non Spring Boot applications. 
References: https://github.com/spring-cloud/spring-cloud-config/issues/299 and https://github.com/spring-cloud/spring-cloud-config/issues/166 


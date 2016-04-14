fcrepo-webapp-plus-cloud
========================


[![Build Status](https://travis-ci.org/fcrepo4-labs/fcrepo-webapp-plus-cloud.png?branch=master)](https://travis-ci.org/fcrepo4-labs/fcrepo-webapp-plus-cloud)

Fcrepo4 webapp plus optional fcrepo dependencies.  This project builds a custom-configured
fcrepo4 webapp war file that includes extra cloud cache dependencies and configuration 
options.  An integration test exists to perform a basic deployment test only and may be 
useful just for identifying syntax errors in configuration file updates or third party 
library version incompatibilities.

# Dependencies
This project has a dependency on the Infinispan Cloud Cache Store, which is not currently available
as a Maven dependency. The [Infinispan Cloud Cache Store](https://github.com/infinispan/infinispan-cachestore-cloud)
project will need to be cloned and built locally. Once cloned, it can be built using:
```
mvn install
```

# Default Maven Build
The default maven build profile is with S3 capability
```
mvn install
```

# Integration Test
By default the maven build will execute a simple integration test which attempts to write
test content to cloud storage. To skip this test during the build, use:
```
mvn install -DskipITs
```
To run the integration test using Amazon S3 storage, set the MAVEN_OPTS environment variable
to include the necessary connection information:
```
MAVEN_OPTS="-Dfcrepo.modeshape.configuration=classpath:/config/s3/repository.json -Dfcrepo.ispn.s3.region=us-standard -Dfcrepo.ispn.s3.accessid=<AWS_ACCESS_ID> -Dfcrepo.ispn.s3.secretkey=<AWS_SECRET_KEY> -Dfcrepo.ispn.s3.bucketprefix=fcrepo-integration-test -Dfcrepo.ispn.s3.endpoint=https://s3.amazonaws.com"
```

# Configuration
To configure and run Fedora against a cloud store, use the [Fedora Application Configuration](https://wiki.duraspace.org/display/FEDORA4x/Application+Configuration)
procedure to define the following properties in the JAVA_OPTS system variable:
```
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.modeshape.configuration=classpath:/config/s3/repository.json"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.ispn.s3.region=us-standard"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.ispn.s3.accessid=<AWS Access ID>"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.ispn.s3.secretkey=<AWS Secret Key>"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.ispn.s3.bucketprefix=<S3 bucket prefix>"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.ispn.s3.endpoint=https://s3.amazonaws.com"
```

# Deployment
Follow the [Fedora Deployment](https://wiki.duraspace.org/display/FEDORA4x/Deploying+Fedora+4+Complete+Guide)
procedure to deploy the WAR which is built by the project.

## Maintainers

* [Bill Branan](https://github.com/bbranan)

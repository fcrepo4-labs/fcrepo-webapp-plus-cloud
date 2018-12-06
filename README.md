fcrepo-webapp-plus-cloud
========================


[![Build Status](https://travis-ci.com/fcrepo4-labs/fcrepo-webapp-plus-cloud.png?branch=master)](https://travis-ci.com/fcrepo4-labs/fcrepo-webapp-plus-cloud)

Fcrepo4 webapp plus options to store binary content in S3.  This project builds a custom-configured
fcrepo4 webapp war file that includes extra dependencies and configuration options.  An integration 
test exists to perform a basic deployment test only and may be useful just for identifying syntax 
errors in configuration file updates or third party library version incompatibilities.

# Dependencies
This project currently has a dependency on the [ModeShape master branch](https://github.com/ModeShape/modeshape), 
which is not available in Maven central. The project will need to be built locally using:
```
mvn install
```
This project also depends on ModeShape 5.x being integrated with the Fedora Repository. This is 
currently available in the [master branch of fcrepo4](https://github.com/fcrepo4/fcrepo4). Fedora will also need to be built locally using:
```
mvn install
```

# Build
Maven is used to build the project. Make sure to build ModeShape and 
Fedora (as noted in Dependencies above) prior to running this build. To build this project, use:
```
mvn install
```
The final result will be the Fedora Repository deployable WAR file with additional S3 binary 
store options.

# Integration Test
By default the maven build will execute a simple integration test which attempts to write
test content to cloud storage. To skip this test during the build, use:
```
mvn install -DskipITs
```
To run the integration test using Amazon S3 storage, set the MAVEN_OPTS environment variable
to include the necessary connection information:
```
MAVEN_OPTS="-Dfcrepo.modeshape.configuration=classpath:/config/s3-file/repository.json -Daws.accessKeyId=<AWS_ACCESS_ID> -Daws.secretKey=<AWS_SECRET_KEY> -Daws.bucket=<AWS_BUCKET>"
```

# Configuration
To configure and run Fedora against a cloud store, use the [Fedora Application Configuration](https://wiki.duraspace.org/display/FEDORA4x/Application+Configuration)
procedure to define properties in the JAVA_OPTS system variable. There are currently 3 different 
configuration paths, each uses Amazon S3 for binary storage, but they vary in where object
storage occurs. Object storage can be set to a file system location or MySQL. There is also the option
to configure Fedora in a cluster, each node of which would share MySQL for object storage and S3 for
binary storage.

These properties are necessary for all configurations:
```
JAVA_OPTS="${JAVA_OPTS} -Daws.accessKeyId=<AWS Access ID>"
JAVA_OPTS="${JAVA_OPTS} -Daws.secretKey=<AWS Secret Key>"
JAVA_OPTS="${JAVA_OPTS} -Daws.bucket=<S3 Bucket Name>"
```

*Choose one of the following*

File object storage:
```
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.modeshape.configuration=classpath:/config/s3-file/repository.json"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.object.directory=<Local Directory>"
```

MySQL object storage:
```
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.modeshape.configuration=classpath:/config/s3-mysql/repository.json"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.mysql.host=<MySQL hostname>"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.mysql.port=<MySQL port>"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.mysql.username=<MySQL username>"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.mysql.password=<MySQL password>"
```

MySQL object storage, clustered:
```
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.modeshape.configuration=classpath:/config/s3-mysql-clustered/repository.json"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.mysql.host=<MySQL hostname>"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.mysql.port=<MySQL port>"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.mysql.username=<MySQL username>"
JAVA_OPTS="${JAVA_OPTS} -Dfcrepo.mysql.password=<MySQL password>"
```

# Deployment
Follow the [Fedora Deployment](https://wiki.duraspace.org/display/FEDORA4x/Deploying+Fedora+4+Complete+Guide)
procedure to deploy the WAR which is built by the project.

## Maintainers

* [Bill Branan](https://github.com/bbranan)

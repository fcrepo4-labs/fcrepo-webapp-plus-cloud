fcrepo-webapp-plus-cloud
========================


[![Build Status](https://travis-ci.org/fcrepo4-labs/fcrepo-webapp-plus-cloud.png?branch=master)](https://travis-ci.org/fcrepo4-labs/fcrepo-webapp-plus-cloud)

Fcrepo4 webapp plus optional fcrepo dependencies.  This project builds a custom-configured
fcrepo4 webapp war file that includes extra cloud cache dependencies and configuration 
options.  An integration test exists to perform a basic deployment test only and may be 
useful just for identifying syntax errors in configuration file updates or third party 
library version incompatibilities.

# Default Maven Build
The default maven build profile is with S3 capability
```
mvn install
```

## Maintainers

* [Bill Branan](https://github.com/bbranan)

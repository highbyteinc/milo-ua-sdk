# Highbyte Fork of Eclipse Milo

Highbyte is java 11 compatible and relies on jaxb 4.0 that depends on jakarta namespace incompatible with olders versions.

No new features are added.

## What is different from the original Eclipse Milo?

* Newer dependency versions:  
  * jakarta.activation-api::2.1.0
  * jaxb-runtime::4.0.4
  * jaxb-maven-plugin::4.0.0  
  * Import updates to account for javax -> jakarta namespace changes 
  * Update autogenerate class location.

## How to change version?
```bash
HB_VERSION=0.6.12-highbyte
mvn versions:set -DnewVersion=${HB_VERSION} -DgenerateBackupPoms=false

cd build-tools
mvn versions:set -DnewVersion=${HB_VERSION} -DgenerateBackupPoms=false
cd -
commit -a -m "Bump version to ${HB_VERSION}"
```
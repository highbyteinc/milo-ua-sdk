# Highbyte Fork of Eclipse Milo

Highbyte is java 11 compatible and relies on jaxb 4.0 that depends on jakarta namespace incompatible with olders versions.

No new features are added.

## What is different from the original Eclipse Milo?

* Newer dependency versions:  
  * jakarta.activation-api::2.1.2
  * jaxb-runtime::4.0.4
  * jaxb-maven-plugin::4.0.0  
  * Import updates to account for javax -> jakarta namespace changes 
  * Update autogenerate class location.

## How to change version?
Use `mvn versions:set` to update to a custom highbyte version, verify the changes with `mvn install`, and then commit.

```bash
# Update 0.6.12 to 0.6.12-highbyte
HB_VERSION=0.6.12-highbyte
mvn versions:set -DnewVersion=${HB_VERSION} -DgenerateBackupPoms=false
cd build-tools
mvn versions:set -DnewVersion=${HB_VERSION} -DgenerateBackupPoms=false
cd -

# Verify the changes and install the jars to local .m2 repo
mvn install

# Commit the change
commit -a -m "[highbyte] Bump version to ${HB_VERSION}"
```

## How to use in your project?

Add a repository to your `pom.xml`:

```xml
<repositories>
    <repository>
        <id>github</id>
        <url>https://maven.pkg.github.com/highbyteinc/milo-ua-sdk</url>
    </repository>
</repositories>
```

Github requires authentication to download packages. You can use a personal access token (PAT) with permission `packages:read` to authenticate with the GitHub Package Registry.

settings.xml:
```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>github</id>
            <username>${env.GITHUB_USER}</username>
            <password>${env.GITHUB_TOKEN}}</password>
        </server>
    </servers>
</settings>
```

When running `mvn` commands, add `-s settings.xml` to the command line to use the settings.xml file.

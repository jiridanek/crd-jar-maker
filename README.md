# crd-jar-maker

This follows the guide at [https://gist.github.com/cleberjamaral/6c9b0a615e51e26c94ffe407a641f531] to host a Maven binary repository in a GitHub repo.

The core of the approach is to deploy a Maven repo structure to a git repository, commit it, push it, and then access it through the `/raw/` GitHub URLs.

To publish single jar to local directory, use approach from [https://maven.apache.org/plugins/maven-install-plugin/examples/specific-local-repo.html]

```
mvn install:install-file -DgroupId=GROUP -DartifactId=ARTIFACT-NAME -Dversion=ARTIFACT-VERSION -Dfile=PATH-TO-THE-JAR -Dpackaging=jar -DlocalRepositoryPath=. -DcreateChecksum=true -DgeneratePom=true
```

To build and publish the `crd-jar-maker` project, assuming you have the following in your project's `pom.xml`,

```
    <distributionManagement>
        <repository>
            <id>mvn-repo</id>
            <url>${repo.url}</url>
        </repository>
    </distributionManagement>
```

use

```
JAVA_HOME=/usr/lib/jvm/java-17-openjdk mvn deploy -Drepo.url=file://$HOME/repos/crd-jar-maker
```

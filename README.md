# Core Entities

## Deploy a snapshot update

We use 
[Sonatype OSSRH](https://central.sonatype.org/pages/ossrh-guide.html)
for hosting, the `~/.m2/settings.xml` should be setup accordingly:

```
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
        https://maven.apache.org/xsd/settings-1.0.0.xsd">

  <profiles>
    <profile>
      <id>sonatype-oss-release</id>
      <properties>
        <gpg.keyname>********</gpg.keyname>
        <gpg.defaultKeyring>true</gpg.defaultKeyring>
        <gpg.useagent>true</gpg.useagent>
        <gpg.lockMode>never</gpg.lockMode>
      </properties>
    </profile>
  </profiles>

  <servers>

    <server>
      <id>sonatype-staging</id>
      <username>********</username>
      <password>********</password>
    </server>

    <server>
      <id>sonatype-snapshot</id>
      <username>********</username>
      <password>********</password>
    </server>

  </servers>

</settings>
```

When this is in place and valid, `mvn deploy` will update the current snapshot artefact.


## Release a new version

We use the
[Maven Release Plugin](https://maven.apache.org/maven-release/maven-release-plugin/)
for packaging and
[Sonatype OSSRH](https://central.sonatype.org/pages/ossrh-guide.html)
for hosting.

The relese plugin requries mostly three steps
(see its documentation for further details):

- `mvn release:clean`
- `mvn release:prepare`
- `mvn release:perform`

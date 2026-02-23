# smarsh-rpm-gradle-build

RPM package providing Java compilation conventions, Spring Boot plugin configuration, repository definitions, and dependency management BOMs.

## Provided Configuration

- Java source/target compatibility (version from `.rpmenv`)
- Spring Boot plugin with `buildInfo()`
- Spring dependency management plugin
- Repository definitions: mavenCentral, mavenLocal, optional Artifactory
- Centralized dependency management BOMs (Spring Cloud, Jackson, etc.)
- Distribution task disabling (distTar, distZip)

## External Plugin Dependencies

Declared in `rpm-manifest.properties`:
- `org.springframework.boot:spring-boot-gradle-plugin:3.5.6`
- `io.spring.gradle:dependency-management-plugin:1.1.6`

## Configuration via `.rpmenv`

Set these in your project's `.rpmenv` file:

```properties
# Java source/target version (default: 17)
JAVA_VERSION=17

# Optional private Maven repository URL (leave empty if not needed)
ARTIFACTORY_URL=https://your-company.jfrog.io/libs-release-local
```

Both values can be overridden by environment variables of the same name.

## Override Dependency Versions

Override centralized dependency versions in your `build.gradle`:
```groovy
ext {
    set('jacksonVersion', '2.18.0')
}
```

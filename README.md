# smarsh-rpm-gradle-build

RPM package providing Java compilation conventions, Spring Boot plugin configuration, repository definitions, and dependency management BOMs.

## Provided Configuration

- Java 17 source/target compatibility
- Spring Boot plugin with `buildInfo()`
- Spring dependency management plugin
- Repository definitions: mavenCentral, mavenLocal, optional Artifactory
- Centralized dependency management BOMs (Spring Cloud, Jackson, etc.)
- Distribution task disabling (distTar, distZip)

## External Plugin Dependencies

Declared in `rpm-manifest.properties`:
- `org.springframework.boot:spring-boot-gradle-plugin:3.5.6`
- `io.spring.gradle:dependency-management-plugin:1.1.6`

## Project-Specific Configuration

Set in your project's `gradle.properties` to add a private repository:
```properties
rpm.artifactory.url=https://your-company.jfrog.io/libs-release-local
```

Override dependency versions in your `build.gradle`:
```groovy
ext {
    set('jacksonVersion', '2.18.0')
}
```

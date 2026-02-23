# smarsh-rpm-gradle-build

RPM package providing Java compilation conventions, Spring Boot plugin configuration, repository definitions, and dependency management BOMs.

## What This Package Does

Applies foundational build configuration that most Java/Spring Boot projects share: Java version, Spring Boot and dependency management plugins, Maven repository definitions, and centralized framework dependency versions. Projects consume this package so their `build.gradle` only contains project-specific dependencies.

## Tasks Provided

| Task | Description |
|---|---|
| `build` | Compile, test, and assemble the project (standard Gradle lifecycle) |
| `bootJar` | Build executable Spring Boot JAR |
| `bootBuildInfo` | Generate `build-info.properties` for Spring Boot Actuator |

## Configs and Assets

| File | Purpose | Synced To |
|---|---|---|
| `build-conventions.gradle` | Plugin application, Java version, repos, dependency management | `.packages/smarsh-rpm-gradle-build/` |
| `rpm-manifest.properties` | Declares external plugin dependencies for buildscript classpath | `.packages/smarsh-rpm-gradle-build/` |

## External Plugin Dependencies

Declared in `rpm-manifest.properties` (resolved by the project's `buildscript {}` block):
- `org.springframework.boot:spring-boot-gradle-plugin:3.5.6`
- `io.spring.gradle:dependency-management-plugin:1.1.6`

## Configuration via `.rpmenv`

Set these in your project's `.rpmenv` file:

```properties
# Java source/target version (required — build fails if not set)
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

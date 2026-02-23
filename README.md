# smarsh-rpm-gradle-build

RPM package providing Java compilation conventions, Spring Boot plugin configuration, and repository definitions.

## What This Package Does

Applies foundational build configuration that most Java/Spring Boot projects share: Java version, Spring Boot and dependency management plugins, and Maven repository definitions.

This package does NOT manage dependency versions (BOMs, library pins). Dependency version management belongs in each project's `build.gradle`. This separation ensures RPM package updates cannot break consumers' dependency trees.

## Tasks Provided

| Task | Description |
|---|---|
| `build` | Compile, test, and assemble the project (standard Gradle lifecycle) |
| `bootJar` | Build executable Spring Boot JAR |
| `bootBuildInfo` | Generate `build-info.properties` for Spring Boot Actuator |

## Configs and Assets

| File | Purpose | Synced To |
|---|---|---|
| `build-conventions.gradle` | Plugin application, Java version, repository definitions | `.packages/smarsh-rpm-gradle-build/` |
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

## Dependency Version Management

This package applies the `io.spring.dependency-management` plugin but does not import any BOMs or pin any dependency versions. Projects must manage their own dependency versions in `build.gradle`:

```groovy
ext {
    set('jacksonVersion', '2.17.2')
    set('springCloudVersion', '2023.0.3')
    testcontainersVersion = '1.19.8'
}

dependencyManagement {
    dependencies {
        dependency 'com.squareup.okhttp3:okhttp:4.10.0'
    }
    imports {
        mavenBom "com.fasterxml.jackson:jackson-bom:${jacksonVersion}"
        mavenBom "org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"
    }
}
```

This approach ensures each project controls its own dependency resolution and RPM package updates cannot introduce version conflicts.

# openapi-generator-parent

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Java 21](https://img.shields.io/badge/Java-21-blue?logo=openjdk)](https://openjdk.org/projects/jdk/21/)
[![Maven](https://img.shields.io/badge/Maven-3.9+-red?logo=apachemaven)](https://maven.apache.org)

Parent POM providing shared build configuration and centralised dependency management for all OpenAPI Generator modules.

---

## Modules

| Module | Description |
|---|---|
| [`openapi-generator-core`](https://github.com/rspereiratech/openapi-generator-core) | Annotation scanning, type hierarchy traversal, schema resolution, and OpenAPI spec assembly |
| [`openapi-generator-maven-plugin`](https://github.com/rspereiratech/openapi-generator-maven-plugin) | Maven plugin that invokes the core generator at build time |
| [`openapi-generator-samples`](https://github.com/rspereiratech/openapi-generator-samples) | Reference Spring MVC application used to validate the plugin |

---

## What This POM Manages

### Dependency Versions

| Dependency | Version |
|---|---|
| `swagger-core` / `swagger-annotations` | 2.2.22 |
| `spring-web` | 6.1.14 |
| `slf4j-api` / `slf4j-simple` | 2.0.13 |
| `lombok` | 1.18.36 |
| `guava` | 33.2.1-jre |
| `maven-plugin-api` / `maven-core` | 3.9.9 |
| `maven-plugin-annotations` | 3.13.1 |
| `junit-jupiter` | 5.11.3 |
| `mockito-junit-jupiter` | 5.14.2 |

### Build Plugin Versions

| Plugin | Version |
|---|---|
| `maven-compiler-plugin` | 3.13.0 |
| `maven-surefire-plugin` | 3.5.2 |
| `maven-plugin-plugin` | 3.13.1 |

### Build Configuration

- Java 21 source and target compatibility
- UTF-8 encoding
- Lombok annotation processor configured on the compiler plugin
- `-parameters` compiler flag enabled (required for Spring MVC parameter name resolution)

---

## Installation

This POM must be installed locally before building any of the child modules:

```bash
git clone git@github.com:rspereiratech/openapi-generator-parent.git
cd openapi-generator-parent
mvn install
```

---

## Usage in Child Modules

```xml
<parent>
  <groupId>io.github.rspereiratech</groupId>
  <artifactId>openapi-generator-parent</artifactId>
  <version>1.0.0-SNAPSHOT</version>
</parent>
```

Child modules inherit all managed dependency versions and build plugin configuration without redeclaring them.

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

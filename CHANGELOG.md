# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] — 2026-03-08

### Added

- Initial parent POM with `groupId` `io.github.rspereiratech`
- Java 21 compiler configuration with UTF-8 encoding and `-parameters` flag
- Lombok annotation processor path configured on `maven-compiler-plugin`
- Managed dependencies:
  - `swagger-core` 2.2.22
  - `swagger-annotations` 2.2.22
  - `spring-web` 6.1.14
  - `slf4j-api` 2.0.13
  - `slf4j-simple` 2.0.13
  - `lombok` 1.18.36 (provided scope)
  - `guava` 33.2.1-jre
  - `maven-plugin-api` 3.9.9 (provided scope)
  - `maven-plugin-annotations` 3.13.1 (provided scope)
  - `maven-core` 3.9.9 (provided scope)
  - `junit-jupiter` 5.11.3 (test scope)
  - `mockito-junit-jupiter` 5.14.2 (test scope)
- Managed build plugins:
  - `maven-compiler-plugin` 3.13.0
  - `maven-surefire-plugin` 3.5.2
  - `maven-plugin-plugin` 3.13.1

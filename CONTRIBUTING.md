# Contributing

This POM has one primary responsibility: keeping dependency and plugin versions consistent across all OpenAPI Generator projects. Contributions are mainly version bumps and the addition of new managed dependencies.

---

## Updating a Dependency Version

All versions are declared as properties at the top of `pom.xml`:

```xml
<properties>
  <swagger-core.version>2.2.22</swagger-core.version>
  <spring.version>6.1.14</spring.version>
  ...
</properties>
```

To update a dependency:

1. Change the version in the `<properties>` block.
2. Install the updated POM locally: `mvn install`.
3. Build and test all dependent projects to verify nothing is broken.
4. Update `CHANGELOG.md` under a new version entry.

---

## Adding a New Managed Dependency

1. Add a `<property>` for the version in the `<properties>` block:

```xml
<my-library.version>1.2.3</my-library.version>
```

2. Add the dependency to `<dependencyManagement>`:

```xml
<dependency>
  <groupId>com.example</groupId>
  <artifactId>my-library</artifactId>
  <version>${my-library.version}</version>
</dependency>
```

3. Child modules can now declare the dependency without specifying a version.
4. Document the addition in `CHANGELOG.md`.

---

## Adding a New Managed Plugin

Add the plugin to `<build><pluginManagement><plugins>`:

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-some-plugin</artifactId>
  <version>${maven-some-plugin.version}</version>
</plugin>
```

---

## Submitting a Pull Request

1. Fork the repository and create a branch from `master`.
2. Make your changes to `pom.xml`.
3. Install locally and verify dependent projects build successfully.
4. Update `CHANGELOG.md`.
5. Open a pull request describing what was changed and why.

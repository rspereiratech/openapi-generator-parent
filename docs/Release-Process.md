# Release Process

This document describes how to publish all projects to Maven Central via Sonatype Central Portal.

## One-Time Setup

### 1. Sonatype Central Portal account

1. Register at [central.sonatype.com](https://central.sonatype.com)
2. Go to **Namespaces** and claim `io.github.rspereiratech`
   - Sonatype will ask you to create a public GitHub repo named after a verification token — follow the on-screen instructions
3. Go to **Account → Generate User Token** and save the `username` and `password`

### 2. GPG key

```bash
# Generate a key (use your personal email)
gpg --full-generate-key

# List keys to get the KEY_ID
gpg --list-secret-keys --keyid-format=long

# Upload the public key to a keyserver so Sonatype can verify signatures
gpg --keyserver keyserver.ubuntu.com --send-keys <KEY_ID>
```

### 3. Maven settings (`~/.m2/settings.xml`)

```xml
<settings>
  <servers>
    <server>
      <id>central</id>
      <username>YOUR_CENTRAL_TOKEN_USERNAME</username>
      <password>YOUR_CENTRAL_TOKEN_PASSWORD</password>
    </server>
  </servers>
</settings>
```

---

## Release Order

The projects must be released in dependency order:

```
1. openapi-generator-parent
2. openapi-generator-core          (depends on parent)
3. openapi-generator-maven-plugin  (depends on parent + core)
```

---

## Releasing

### Step 1 — parent

```bash
cd openapi-generator-parent
mvn deploy -P release -DskipTests
```

### Step 2 — core

```bash
cd openapi-generator-core
mvn deploy -P release -DskipTests
```

### Step 3 — plugin

```bash
cd openapi-generator-maven-plugin
mvn deploy -P release -DskipTests
```

Each `deploy` will sign the artifacts with GPG, upload them to Sonatype Central Portal, and wait until they are published to Maven Central.

---

## After Release

- Create a GitHub Release on each repo matching the version tag
- Artifacts appear on [Maven Central](https://search.maven.org/search?q=g:io.github.rspereiratech) within a few minutes

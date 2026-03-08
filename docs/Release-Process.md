# Release Process

This document describes how to publish all projects to Maven Central via Sonatype Central Portal.

## One-Time Setup

### 1. Sonatype Central Portal account

1. Register at [central.sonatype.com](https://central.sonatype.com)
2. Go to **Namespaces** and claim `io.github.rspereiratech`
   - Sonatype will ask you to create a public GitHub repo named after a verification token — follow the on-screen instructions
3. Once verified, go to **Account → Generate User Token** and save the `username` and `password` — these are your `CENTRAL_USERNAME` and `CENTRAL_TOKEN` secrets

### 2. GPG key

```bash
# Generate a key (use your personal email)
gpg --full-generate-key

# List keys to get the KEY_ID
gpg --list-secret-keys --keyid-format=long

# Export public key and upload to keyserver
gpg --keyserver keyserver.ubuntu.com --send-keys <KEY_ID>

# Export private key for GitHub secret
gpg --armor --export-secret-keys <KEY_ID> > gpg-private-key.asc
```

### 3. GitHub Secrets

Add the following secrets to each repo that publishes to Maven Central (`openapi-generator-parent`, `openapi-generator-core`, `openapi-generator-maven-plugin`):

| Secret | Description |
|--------|-------------|
| `CENTRAL_USERNAME` | Sonatype Central Portal user token username |
| `CENTRAL_TOKEN` | Sonatype Central Portal user token password |
| `GPG_PRIVATE_KEY` | Contents of `gpg-private-key.asc` |
| `GPG_PASSPHRASE` | Passphrase used when generating the GPG key |
| `PAT_TOKEN` | GitHub Personal Access Token with `repo` scope (needed to checkout private repos in CI) |

To add secrets: **GitHub repo → Settings → Secrets and variables → Actions → New repository secret**

---

## Release Order

The projects must be released in dependency order:

```
1. openapi-generator-parent
2. openapi-generator-core      (depends on parent)
3. openapi-generator-maven-plugin  (depends on parent + core)
```

---

## Releasing a Project

### Automated (recommended)

Push a version tag to trigger the release workflow:

```bash
git tag v1.0.0
git push origin v1.0.0
```

The GitHub Actions release workflow will:
1. Check out the repo and bootstrap dependencies
2. Sign all artifacts with GPG
3. Deploy to Sonatype Central Portal
4. Wait until the artifacts are published to Maven Central

### Manual

```bash
# Make sure dependencies are already installed locally
mvn install -f ../openapi-generator-parent/pom.xml -DskipTests  # if needed
mvn install -f ../openapi-generator-core/pom.xml -DskipTests    # if needed

# Deploy with the release profile
mvn deploy -P release -DskipTests
```

This requires a `~/.m2/settings.xml` with the central server credentials:

```xml
<settings>
  <servers>
    <server>
      <id>central</id>
      <username>YOUR_CENTRAL_USERNAME</username>
      <password>YOUR_CENTRAL_TOKEN</password>
    </server>
  </servers>
</settings>
```

---

## After Release

- Artifacts appear on [Maven Central](https://search.maven.org/search?q=g:io.github.rspereiratech) within a few minutes
- Update `CHANGELOG.md` with the release date
- Create a GitHub Release matching the tag

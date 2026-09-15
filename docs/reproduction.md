Set up a minimal Maven reproduction repo named `jreleaser-git-remote-ignored` for the JReleaser git-remote issue.

Requirements:

* Use the local `./mvnw` CLI for all Maven commands.
* Put the entire JReleaser configuration in `pom.xml`. Do not create any YAML config.
* Use JReleaser Maven Plugin `1.26.0`:

```xml
<plugin>
  <groupId>org.jreleaser</groupId>
  <artifactId>jreleaser-maven-plugin</artifactId>
  <version>1.26.0</version>
</plugin>
```

* Keep the project minimal and focus only on the Git tag part of `jreleaser:release`.
* Configure the GitHub releaser so that artifacts/releases/assets are skipped, but tag creation is enabled:

```xml
<artifacts>false</artifacts>
<tagName>${gitlab.release.tagName}</tagName>
<skipTag>false</skipTag>
<skipRelease>true</skipRelease>
<uploadAssets>NEVER</uploadAssets>
```

* Do not configure Git remotes. I will manually add two remotes later: one SSH remote and one HTTPS remote.
* Ensure the repo is ready to reproduce the problem with:

```bash
export JRELEASER_DEFAULT_GIT_REMOTE=jreleaser-https
export SOURCE_REPO_GITHUB_USERNAME=""
export SOURCE_REPO_GITHUB_TOKEN=""

./mvnw jreleaser:release \
  -Djreleaser.github.username="$SOURCE_REPO_GITHUB_USERNAME" \
  -Djreleaser.github.token="$SOURCE_REPO_GITHUB_TOKEN" \
  -Djreleaser.upload.active=NEVER
```

* Before finishing, self-verify the setup by running JReleaser in dry-run mode with `./mvnw jreleaser:release -Djreleaser.dry.run=true` and fix any configuration errors it reports.

Create all minimal files needed, validate the Maven setup using `./mvnw`, and keep the repository intentionally small and reproduction-focused.

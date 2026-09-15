# jreleaser-git-remote-ignored

Minimal reproduction for a JReleaser Git remote tagging issue.

* Issue: [TODO](TODO)
* Related reference: [JRELEASER_DEFAULT_GIT_REMOTE ignored during tagging 1434](https://github.com/jreleaser/jreleaser/issues/1434)

See [`docs/reproduction.md`](docs/reproduction.md) for reproduction steps.

## Setup devenv using mise

```bash
mise install
mise exec -- java -version
# If you do not have the shell integration:
mise use
java -version
./mvnw --version
```

### Setup the mise shell integration

For zsh:

```
echo 'eval "$(mise activate zsh)"' >> ~/.zshrc
source ~/.zshrc
```

For bash:

```
echo 'eval "$(mise activate bash)"' >> ~/.bashrc
source ~/.bashrc
```

Dry run:

```
set -a
source .env
set +a

./mvnw jreleaser:release \
  -Djreleaser.github.username="$SOURCE_REPO_GITHUB_USERNAME" \
  -Djreleaser.github.token="$SOURCE_REPO_GITHUB_TOKEN" \
  -Djreleaser.upload.active=NEVER \
  -Djreleaser.dry.run=true
```

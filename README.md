# jreleaser-git-remote-ignored

Minimal reproduction for a JReleaser Git remote tagging issue.

* Issue: [JRELEASER_DEFAULT_GIT_REMOTE ignored during tagging v2](https://github.com/jreleaser/jreleaser/issues/2170)
* Related reference: [JRELEASER_DEFAULT_GIT_REMOTE ignored during tagging 1434](https://github.com/jreleaser/jreleaser/issues/1434)

See [`docs/reproduction.md`](docs/reproduction.md) for reproduction steps.

## Git remotes

```bash
git clone git@github.com:Adito5393/jreleaser-git-remote-ignored.git
# or: git clone https://github.com/Adito5393/jreleaser-git-remote-ignored.git
cd jreleaser-git-remote-ignored

git remote rename origin upstream
git remote add jreleaser-https https://github.com/Adito5393/jreleaser-git-remote-ignored.git
git remote add jreleaser-ssh git@github.com:Adito5393/jreleaser-git-remote-ignored.git
```

Skip a `git remote add` if that URL is already present after the clone. There must be no `origin` remote. Tagging still looks up `origin` and fails with `origin: not found.`

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
mise run jreleaser:dry-run
```

Full reproduction (creates a tag):

```
mise run jreleaser:release
```

## Without mise

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

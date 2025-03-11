<h2 align="center">
  <br>
  <p align="center"><img src="https://raw.githubusercontent.com/rebound-how/cli/main/public/logo.png"></p>
</h2>

<h4 align="center">Rebound GitHub Actions | The open source toolbox for resilient operations</h4>

<p align="center">
   <a href="https://github.com/rebound-how/actions/blob/master/LICENSE.md">
   <img alt="License" src="https://img.shields.io/github/license/reliablyhq/cli">
</p>

<p align="center">
  <a href="#installation">Installation</a> •
  <a href="https://reliably.com/docs/cli/">Documentation</a>
</p>

---

Rebound is your open-source toolbox to help you building resilient operations.

# Actions

## lueur

[lueurscenario]: https://lueur.dev/docs/

The main action in this repository is the `lueur` action. It features:

* Runs [lueur scenarios](lueurscenario) from within a GitHub workflow

The basic action usage is as follows:

```yaml
name: Execute a lueur scenario file

on:
  workflow_dispatch:

jobs:
  run-reliability-scenario
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - uses: rebound-how/actions@main
```

Store this as a workflow called `lueur.yaml`.

[More information](https://reliably.com/docs/deployment/#github-1)

The Rebound lueur Action has properties which are passed to the underlying
script. These are passed to the action using `with`.

| Property | Default | Description |
| --- | --- | --- |
| github-token | | GitHub token with enough permissions to commit to the repository. Usually set it with `${{ secrets.GITHUB_TOKEN }}` |

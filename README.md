<h2 align="center">
  <br>
  <p align="center"><img src="https://raw.githubusercontent.com/rebound-how/www/main/public/social.png"></p>
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
  run-reliability-scenario:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - uses: rebound-how/actions/lueur@main
```

Store this as a workflow called `lueur.yaml`.

[More information](https://reliably.com/docs/deployment/#github-1)

The Rebound lueur Action has properties which are passed to the underlying
script. These are passed to the action using `with`.

| Property | Required | Default | Description |
| --- | --- | --- | --- |
| scenario | Yes | | Path to a single [lueur scenario file][lueurscenario] or a directory containing scenario files |
| report | No | report.md | Path to the file where to store the generated report. The extension determines the type of report generated. |
| result | No | result.json | Path to the file containing the events and traces from the scenario runs. |


## Reliably

[plan]: https://reliably.com/docs/concepts/plans/

The main action in this repository is the `plan` action. It features:

* Runs [Reliably plan](plan) from within a GitHub workflow
* Allows you to keep your sensitive data in a GitHub Environment so that
  you keep them close to your operations
* Reports its results back to Reliably
* Stores the result files (the log and journal) as a commit in the repository
* Stores a file listing all the licences of all the packages used as part
  of run within the commit

The basic action usage is as follows:

```yaml
name: Execute a Reliably Plan

on:
  workflow_dispatch:

jobs:
  execute-reliably-plan:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - uses: rebound-how/actions/reliably@main
```

Store this as a workflow called `reliably-plan.yaml`.

[More information](https://reliably.com/docs/deployment/#github-1)

The Reliably Plan Action has properties which are passed to the underlying script.
These are passed to the action using `with`.

| Property | Default | Description |
| --- | --- | --- |
| python-version | "3.11" | Run Reliably using this version of Python (3.11+) |
| github-token | | GitHub token with enough permissions to commit to the repository. Usually set it with `${{ secrets.GITHUB_TOKEN }}` |
| reliably-service-token | | Reliably token to authenticate with Reliably services. Usually set it with `${{ secrets.RELIABLY_SERVICE_TOKEN }}` |
| reliably-host | | The Reliably host. Only useful if you run Reliably on your own host |
| org-id | | Reliably organization identifier for this run |
| plan-id | | Reliably plan identifier for this run |
| working-dir | "./plans" | Repository relative directory where to run the plan from |
| reliably-experiment-extra | | A JSOn encoded object loaded by reliably to add to the results |
| dependencies | | Various dependencies to install. Comma-separated list from: oha, aws-authenticator, lueur |


### Various notes

* The action automatically installs the Reliably CLI and many
  [Chaos Toolkit extensions](ctk) for you
* If you create a `bin` directory at the top of your repository, the
  action will automatically add it to the `PATH` if your plan requires access
  to specific utilities.
* The action can download:
  * [aws-iam-authenticator](https://github.com/kubernetes-sigs/aws-iam-authenticator) binary for you so you can authenticate against AWS EKS clusters
  * [lueur](https://github.com/rebound-how/rebound/tree/main/lueur) binary to run a proxy that injects network faults
  * [oha](https://github.com/hatoo/oha) binary to run load tests


[ctk]: https://github.com/rebound-how/actions/blob/main/reliably/pyproject.toml#L7
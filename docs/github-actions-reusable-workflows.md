<!-- markdownlint-disable -->



## Features branch (Pull request) workflow 

Perform CI - lint `action.yml` and run tests 

### Usage 

Create in your repo  __`.github/workflows/feature.yaml`__

```yaml
  name: Feature branch
  on:
    pull_request:
      branches: [ main ]
      types: [opened, synchronize, reopened]

  jobs:
    perform:
      uses: cloudposse/github-actions-workflows-github-action-composite/.github/workflows/feature-branch.yml@main
      with:
        organization: "&#36;{{ github.event.repository.owner.login }}"
        repository: "&#36;{{ github.event.repository.name }}"
        ref: "&#36;{{ github.event.pull_request.head.ref  }}"
      secrets:
        github-private-actions-pat: "&#36;{{ secrets.PUBLIC_REPO_ACCESS_TOKEN }}"
```



### Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| organization | Repository owner organization (ex. acme for repo acme/example) | string | ${{ github.event.repository.owner.login }} | false |
| ref | The fully-formed ref of the branch or tag that triggered the workflow run | string | ${{ github.ref }} | false |
| repository | Repository name (ex. example for repo acme/example) | string | ${{ github.event.repository.name }} | false |
| tests-prefix | Workflows file name prefix to run as tests | string | test-\* | false |



### Secrets

| Name | Description | Required |
|------|-------------|----------|
| github-private-actions-pat | Github PAT allow to trigger workflows for testing | true |






## Main branch workflow

Lint `action.yml`, run tests and draft release

### Usage 

Create in your repo  __`.github/workflows/main.yaml`__

```yaml
  name: Main branch
  on:
    push:
      branches: [ main ]

  permissions:
    contents: write

  jobs:
    perform:
      uses: cloudposse/github-actions-workflows-github-action-composite/.github/workflows/main-branch.yml@main
      with:
        organization: "&#36;{{ github.event.repository.owner.login }}"
        repository: "&#36;{{ github.event.repository.name }}"
      secrets:
        github-private-actions-pat: "&#36;{{ secrets.PUBLIC_REPO_ACCESS_TOKEN }}"
```



### Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| organization | Repository owner organization (ex. acme for repo acme/example) | string | ${{ github.event.repository.owner.login }} | false |
| ref | The fully-formed ref of the branch or tag that triggered the workflow run | string | ${{ github.ref }} | false |
| repository | Repository name (ex. example for repo acme/example) | string | ${{ github.event.repository.name }} | false |
| tests-prefix | Workflows file name prefix to run as tests | string | test-\* | false |



### Secrets

| Name | Description | Required |
|------|-------------|----------|
| github-private-actions-pat | Github PAT allow to trigger workflows for testing | true |





<!-- markdownlint-restore -->

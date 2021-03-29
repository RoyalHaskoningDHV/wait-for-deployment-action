# Wait for deployment GitHub Action

This action blocks until a deployment is ready for your push, and outputs its
URL so that you can run tests and other checks against a live site without
running it in Actions.

## Setup

```yml
name: Test
on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: RoyalHaskoningDHV/wait-for-deployment-action@v3
        id: deployment
        with:
          token: ${{ github.token }}
          environment: Preview

      - run: echo "Deployed to: ${{ steps.deployment.outputs.url }}"
```

## Inputs

### `token`
This is your GitHub access token, typically accessible via `${{ github.token }}`.

### `environment`
This is the deployment environment to target.

### `sha`
The SHA of the commit being deployed.

**TODO:** document how to set the environment conditionally.

### `timeout`
The number of seconds after which to give up with an error. Default: 30.

### `interval`
The number of seconds to wait between polls to the deployments API. Default: 5.

## Outputs

### `url`
The target URL of the deployment, if found.

### `id`
The id of the deployment.

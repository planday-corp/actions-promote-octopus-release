# Actions Promote Octopus Release

This repository contains a reusable GitHub workflow to promote a release to an environment in Octopus Deploy.

## Inputs

| Name | Type | Required | Description |
| :---: | :---: | :---: |  --- |
| `project_name` | `string` | `true` | Name or ID of the Octopus project (ex: `Planday.Domain.Api`) |
| `deploy_to` | `string` | `true` | Name or ID of the environment to deploy to (ex: `stable`) |
| `release_number` | `string` | `true` | Version number of the release to deploy |
| `space` | `string` | `false` | The name or ID of the space within which to deploy the release into. Defaults to the `Default` space if left empty |
| `octopus_extra_args` | `string` | `false` | Any additional arguments to pass to the `octo deploy-release` command. Default:`--progress --waitForDeployment` |

## Secrets

| Name | Required | Description |
| :---: | :---: |  --- |
| `octopus_server_url` | `true` | The URL of the Octopus server |
| `octopus_api_key` | `true` | API key of the Octopus server |

## Outputs

| Name | Description |
| :---: | --- |
| `release_number` | Version number of the release deployed |
| `environment` | Name or ID of the environment deployed to |


## Usage

```yaml
jobs:
  promote-staging:
    uses: planday-corp/actions-promote-octopus-release/.github/workflows/promote_release.yml@v1
    with:
      project_name: Planday.Domain.Api
      deploy_to: Staging
      release_number: "2.1.3"
      space: Default
      octopus_extra_args: "--waitForDeployment --noRawLog"
    secrets:
      octopus_server_url: ${{secrets.OCTOPUSSERVERURL}}
      octopus_api_key: ${{secrets.OCTOPUSSERVERAPIKEY}}
```
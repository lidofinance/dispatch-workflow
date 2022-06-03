# dispatch-workflow

Custom GitHub action to trigger action execution in the external repo

## Usage

Using tag reference:

```
    steps:
      - name: Build prod image
        uses: lidofinance/dispatch-workflow@v1
        env:
          APP_ID: <GitHub App ID>
          APP_PRIVATE_KEY: <GitHub App private key>
          TARGET_REPO: "org/repo"
          TARGET_WORKFLOW: <filename of the workflow in the TARGET_REPO>
          TAG: <git tag to checkout>
```

Using generic reference:

```
    steps:
      - name: Build prod image
        uses: lidofinance/dispatch-workflow@v1
        env:
          APP_ID: <GitHub App ID>
          APP_PRIVATE_KEY: <GitHub App private key>
          TARGET_REPO: "org/repo"
          TARGET_WORKFLOW: <filename of the workflow in the TARGET_REPO>
          TARGET: <git ref to checkout>
```

**NOTE** TAG and TARGET env vars will be converted to workflow inputs 'tag' and 'repo_ref' respectively. Make sure that
you have this inputs in the target workflow. ex:

```
name: Awesome WF

on:
  workflow_dispatch:
    inputs:
      repo_ref:
        description: "Target git repo ref"
        default: master
        required: true
```

or

```
name: Even more awesome WF

on:
  workflow_dispatch:
    inputs:
      tag:
        description: "tag to build and upload"
        required: true
```

### Additional inputs

Any additional inputs can be passed using env vars with **INPUTS_** prefix. ex:

```
    steps:
      - name: Build prod image
        uses: lidofinance/dispatch-workflow@v1
        env:
          APP_ID: <GitHub App ID>
          APP_PRIVATE_KEY: <GitHub App private key>
          TARGET_REPO: "org/repo"
          TARGET_WORKFLOW: <filename of the workflow in the TARGET_REPO>
          INPUTS_AWESOME_VAR: <Awesome var value>
```

```
name: Some WF

on:
  workflow_dispatch:
    inputs:
      awesome_var:
        description: "some awesome var"
```
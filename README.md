# devbox-install-action

This action downloads the devbox CLI and installs the Nix packages defined in your `devbox.json`.

[![version](https://img.shields.io/github/v/release/jetify-com/devbox-install-action?color=green&label=version&sort=semver)](https://github.com/jetify-com/devbox-install-action/releases) [![tests](https://github.com/jetify-com/devbox-install-action/actions/workflows/test.yaml/badge.svg)](https://github.com/jetify-com/devbox-install-action/actions/workflows/test.yaml?branch=main)

## Example Workflow

```
name: Testing with devbox

on: push

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Install devbox
        uses: open-turo/devbox-install-action
        with:
          s3-bucket-name: devbox-cache-bucket
          s3-bucket-region: us-east-1
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

      - name: Run arbitrary commands
        run: devbox run -- echo "done!"

      - name: Run a script called test
        run: devbox run test
```

## Configure Action

### Action Inputs

| Input argument           | description                                                                           | default               |
|--------------------------|---------------------------------------------------------------------------------------|-----------------------|
| project-path             | Path to the folder that contains a valid `devbox.json`                                | repo's root directory |
| enable-cache             | Cache the entire Nix store in github based on your `devbox.json`                      | true                  |
| refresh-cli              | Specify whether the CLI should be redownloaded                                        | false                 |
| devbox-version           | Specify devbox CLI version you want to pin to. Only supports >0.2.2                   | latest                |
| sha256-checksum          | Specify an explicit checksum for the devbox binary                                    |                       |
| disable-nix-access-token | Disable configuration of nix access-tokens with the GitHub token used in the workflow | false                 |
| skip-nix-installation    | Skip the installation of nix                                                          | false                 |
| use-fallback-cache       | Use the fallback cache if the s3 bucket cache is not available                        | true                  |
| s3-bucket-name           | Specify the name of the s3 bucket to use for caching                                  |                       |
| aws-region               | Specify the region of the s3 bucket to use for caching                                |                       |
| aws-access-key-id        | Specify the access key id for the s3 bucket to use for caching                        |                       |
| aws-secret-access-key    | Specify the secret access key for the s3 bucket to use for caching                    |                       |
| aws-session-token        | Specify the session token for the s3 bucket to use for caching                        |                       |

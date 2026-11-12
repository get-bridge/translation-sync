# translation-sync

![ci](https://github.com/get-bridge/translation-sync/workflows/ci/badge.svg)
![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/get-bridge/translation-sync?sort=semver)

Sync translation files to and from an s3-compatible remote bucket. This uses the
[@get-bridge/sync-format-message-translations](https://github.com/get-bridge/sync-format-message-translations) npm package and thus requires authentication with
Github Packages.

## Usage

### With OIDC (default)

OIDC is enabled by default — just add `permissions: id-token: write` to your job:

```yaml
permissions:
  id-token: write
  contents: read

steps:
  - uses: actions/setup-node@v4
    with:
      node-version-file: '.nvmrc'
      scope: '@get-bridge'
      registry-url: https://npm.pkg.github.com

  - uses: get-bridge/translation-sync@v2
    with:
      config: src/i18n/sync.json
    env:
      NODE_AUTH_TOKEN: ${{ secrets.GIT_HUB_PACKAGES_TOKEN }}
```

### With static credentials (legacy)

To use static credentials instead of OIDC, set `role-to-assume` to an empty string:

```yaml
steps:
  - uses: actions/setup-node@v4
    with:
      node-version-file: '.nvmrc'
      scope: '@get-bridge'
      registry-url: https://npm.pkg.github.com

  - uses: get-bridge/translation-sync@v2
    with:
      config: src/i18n/sync.json
      role-to-assume: ''
    env:
      AWS_ACCESS_KEY_ID: ${{ secrets.BRIDGE_TRANSLATIONS_AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.BRIDGE_TRANSLATIONS_AWS_SECRET_ACCESS_KEY }}
      NODE_AUTH_TOKEN: ${{ secrets.GIT_HUB_PACKAGES_TOKEN }}
```

## Inputs

Note: the `NODE_AUTH_TOKEN` environment variable must be present, otherwise authorization with the `@get-bridge` registry will fail.

| Name              | Required | Default                                                              | Description                                                                                     |
|-------------------|----------|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| `config`          | false    | `translation-sync.json`                                              | Path to the JSON-formatted configuration file.                                                  |
| `role-to-assume`  | false    | `arn:aws:iam::127178877223:role/github/github-translations`          | IAM role ARN to assume via GitHub OIDC. Set to empty string to disable OIDC.                    |
| `aws-region`      | false    | `us-east-1`                                                          | AWS region for the S3 buckets.                                                                  |

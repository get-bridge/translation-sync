# translation-sync

![ci](https://github.com/get-bridge/translation-sync/workflows/ci/badge.svg)
![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/get-bridge/translation-sync?sort=semver)

Sync translation files to and from an s3-compatible remote bucket. This uses
`@get-bridge/sync-format-message-translations` and thus requires authentication with
Github Packages.

## Usage

    - uses: actions/setup-node@v2.4.0
      with:
        node-version: 14
        scope: '@get-bridge'
        registry-url: https://npm.pkg.github.com

    - uses: get-bridge/translation-sync@v1.0.1
      env:
        NODE_AUTH_TOKEN: <token>
      with:
        config: test/fixtures/config.json

## Customizing

### Inputs

Note: the NODE_AUTH_TOKEN environemnt variable must be present otherwise authorization with the `@get-bridge` registry will fail.

- `config`: *Optional* – default: `translation-sync.json`
  The path to the JSON-formatted configuration file. See
  `@get-bridge/sync-format-message-translations`'s own documentation for details.

The following inputs can be used as `step.with` keys or via the corresponding environment variable. The `steps.with` values will take precidence over equivalent environment variables.

| Name      | env var                    | Required  | Default                  | Type    | Description                         |
|-----------|----------------------------|-----------|--------------------------|---------|-------------------------------------|
| `config`  | `TRANSLATION_SYNC_CONFIG`  | false     | `translation-sync.json`  | String  | Email associated with the username  |

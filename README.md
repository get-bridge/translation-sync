# translation-sync

![ci](https://github.com/get-bridge/translation-sync/workflows/ci/badge.svg)
![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/get-bridge/translation-sync?sort=semver)

Sync translation files to and from an s3-compatible remote bucket. This uses
`@inst/sync-format-message-tranlations` and thus requires authentication with
our internal npm registry. For an example configuration file, see
[config.json](test/fixtures/config.json)

## Usage

    - uses: get-bridge/npm-login@v1
      with:
        email: ${{ secrets.INSTRUCTURE_NPM_EMAIL }}
        password: ${{ secrets.INSTRUCTURE_NPM_PASSWORD }}
        registry: ${{ secrets.INSTRUCTURE_NPM_REGISTRY }}
        scope: inst
        username: ${{ secrets.INSTRUCTURE_NPM_USERNAME }}
    - uses: get-bridge/translation-sync@v1.0.0
      with:
        config: test/fixtures/config.json

## Customizing

### inputs

- `config`: *Optional* – default: `translation-sync.json`
  The path to the JSON-formatted configuration file. See
  `@inst/sync-format-message-translations`'s own documentation for details.

The following inputs can be used as `step.with` keys or via the corresponding environment variable. The `steps.with` values will take precidence over equivalent environment variables.

| Name      | env var                    | Required  | Default                  | Type    | Description                         |
|-----------|----------------------------|-----------|--------------------------|---------|-------------------------------------|
| `config`  | `TRANSLATION_SYNC_CONFIG`  | false     | `translation-sync.json`  | String  | Email associated with the username  |

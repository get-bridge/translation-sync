# translation-sync

![ci](https://github.com/get-bridge/translation-sync/workflows/ci/badge.svg)
![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/get-bridge/translation-sync?sort=semver)

Sync translation files to and from an s3-compatible remote bucket. This uses
`@get-bridge/sync-format-message-translations` and thus requires authentication with
Github Packages.

## Usage

    - name: Configure private repositories
      # there are several bugs in npm 6.14.x that prevented us from using `npm config` for now
      run: |
        tee -a ~/.npmrc << END
        @get-bridge:registry=https://npm.pkg.github.com/
        //npm.pkg.github.com/:_authToken=\${BRIDGE_GITHUB_PACKAGES_NPM_AUTH_TOKEN}
        END
    - uses: get-bridge/translation-sync@v1.0.0
      with:
        config: test/fixtures/config.json

## Customizing

### inputs

- `config`: *Optional* – default: `translation-sync.json`
  The path to the JSON-formatted configuration file. See
  `@get-bridge/sync-format-message-translations`'s own documentation for details.

The following inputs can be used as `step.with` keys or via the corresponding environment variable. The `steps.with` values will take precidence over equivalent environment variables.

| Name      | env var                    | Required  | Default                  | Type    | Description                         |
|-----------|----------------------------|-----------|--------------------------|---------|-------------------------------------|
| `config`  | `TRANSLATION_SYNC_CONFIG`  | false     | `translation-sync.json`  | String  | Email associated with the username  |

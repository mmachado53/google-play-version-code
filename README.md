# Next version code in google play console action

This action looks for the next valid version number to upload a new app or bundle in the play store console

## Inputs

### `serviceAccountJsonFile`

**Required** the path of the `service-account.json` file.

### `packageName`

**Required** The Application Id of the app.

## Outputs

### `versionCode`

The next valid version number to upload a new apk or bundle

## Example usage

### Basic

```yaml
- uses: mmachado53/google-play-next-version-code@v0.0.5
  id: next_version_code
  with:
    serviceAccountJsonFile: ./service-account.json
    packageName: com.your.packageName
```

### building the `service-account.json` from some secret example

```yaml
- name: building service_account.json
  run: echo '${{ secrets.GOOGLE_PLAY_SERVICE_ACCOUNT_JSON }}' > service_account.json
- uses: mmachado53/google-play-next-version-code@v0.0.5
  id: next_version_code
  with:
    serviceAccountJsonFile: service-account.json
    packageName: com.your.packageName
```

### Putting the version number in the code

```yaml
- name: building service-account.json
  run: echo '${{ secrets.GOOGLE_PLAY_SERVICE_ACCOUNT_JSON }}' > service-account.json
- uses: mmachado53/google-play-next-version-code@v0.0.5
  id: next_version_code
  with:
    serviceAccountJsonFile: service-account.json
    packageName: com.your.packageName
- name: Putting version code into app/build.gradle
  uses: chkfung/android-version-actions@v1.2.2
  with:
    gradlePath: app/build.gradle
    versionCode: ${{steps.next_version_code.outputs.versionCode}}
```


# Run Node Tests Action

This GitHub Action sets up a Node.js environment and runs install, audit, test, and build commands for your Node.js project.

## Usage

Example usage in a workflow:

```yaml
name: Node.js CI

on:
  pull_request:
    branches:
      - main
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  node-tests:
    if: github.event.pull_request.draft == false
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
    - uses: actions/checkout@v4

    - name: Run Node Tests in src directory
      uses: alleyinteractive/action-test-node@v1
      with:
        node: 'lts/*'
        working-directory: './src'
        cache-dependency-path: './src/package-lock.json'
        skip-audit: 'true'
        test-command: 'npm run test:ci && npm run test:coverage'
        build-command: 'npm run build:prod'
```


## Inputs

> Specify using `with` keyword.

### `node-version`

- Specify the Node.js version to use.
- Accepts a string.
- Defaults to `lts/*`.

### `npm-version`

- Specify the npm version to use if different from the bundled version.
- Accepts a string.
- Defaults to an empty string, which uses the default npm version.

### `working-directory`

- Specify the directory to run the commands in.
- Accepts a string.
- Defaults to `.`.

### `cache-dependency-path`

- Specify the path to the dependency file to use for caching.
- Accepts a string.
- Defaults to `package-lock.json`.

### `audit-skip`

- Determine whether to skip the npm audit step.
- Accepts a boolean string (`'true'` or `'false'`).
- Defaults to `'false'`, which runs the audit step.

### `audit-command`

- Specify the command to run for npm audit.
- Accepts a string.
- Defaults to `npm audit --audit-level=high --production`.

### `install-skip`

- Determine whether to skip the npm install step.
- Accepts a boolean string (`'true'` or `'false'`).
- Defaults to `'false'`, which runs the install step.

### `install-command`

- Specify the command to run for npm install.
- Accepts a string.
- Defaults to `npm ci`.

### `test-skip`

- Determine whether to skip the test step.
- Accepts a boolean string (`'true'` or `'false'`).
- Defaults to `'false'`, which runs the test step.

### `test-command`

- Specify the command to run for tests.
- Accepts a string.
- Defaults to `npm test`.

### `build-skip`

- Determine whether to skip the build step.
- Accepts a boolean string (`'true'` or `'false'`).
- Defaults to `'false'`, which runs the build step.

### `build-command`

- Specify the command to run for build.
- Accepts a string.
- Defaults to `npm run build`.

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed
recently.

## Credits

This project is actively maintained by [Alley
Interactive](https://github.com/alleyinteractive).

- [Ben Bolton](https://github.com/benpbolton)
- [All Contributors](../../contributors)

## License

The GNU General Public License (GPL) license. Please see [License File](LICENSE)
for more information.⏎
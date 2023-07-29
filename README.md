# lintrunner-action

The action sets up and runs `lintrunner`(https://github.com/suo/lintrunner) to lint the whole repository.

`lintrunner` is a tool that runs linters. It provides a uniform linting experience in CI and in local dev environments. Visit https://github.com/suo/lintrunner to learn more about `lintrunner` and https://github.com/justinchuby/lintrunner-adapters to see the list of supported linters, as well as a simple guide on how to create support for new linters.

## Usage

See [action.yml](./action.yml)

```yaml
steps:
  - uses: actions/checkout@v3
  - uses: justinchuby/lintrunner-action@main
    with:
      # Whether the action should upload a SARIF report of the
      # lint results which will show up as a GitHub code scanning report
      publish_code_scanning: true
      # Disable verbose logging from lintrunner and only show lint results
      quiet: true
```

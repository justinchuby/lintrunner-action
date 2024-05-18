# lintrunner-action

This action sets up and runs `lintrunner`(https://github.com/suo/lintrunner) to lint the whole repository.

`lintrunner` is a tool that runs linters with auto-fix support. It provides a uniform linting experience in CI and in local dev environments. Visit https://github.com/suo/lintrunner to learn more about `lintrunner` and https://github.com/justinchuby/lintrunner-adapters to see the list of supported linters, as well as a simple guide on how to create support for new linters.

## Usage

See [action.yml](./action.yml)

```yaml
jobs:
  lint:
    permissions:
      security-events: write
    runs-on: ubuntu-latest
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

## Set up lintrunner

To set up `lintrunner`, create a `.lintrunner.toml` configuration file in the root of the repository. An example linter configuration looks like:

```toml
merge_base_with = 'main'

[[linter]]
code = 'RUFF'
include_patterns = [
    '**/*.py',
    '**/*.pyi',
]
exclude_patterns = [
]
command = [
    'python',
    '-m',
    'lintrunner_adapters',
    'run',
    'ruff_linter',
    '--config=pyproject.toml',
    '@{{PATHSFILE}}'
]
init_command = [
    'python',
    '-m',
    'lintrunner_adapters',
    'run',
    'pip_init',
    '--dry-run={{DRYRUN}}',
    '--requirement=requirements/lintrunner/requirements.txt',
]
is_formatter = true
```

Visit https://github.com/suo/lintrunner for a complete setup guide and https://github.com/pytorch/pytorch/wiki/lintrunner for more documentation.

### Example configs

- https://github.com/justinchuby/lintrunner-adapters/blob/main/.lintrunner.toml
- https://github.com/pytorch/pytorch/blob/main/.lintrunner.toml
- https://github.com/microsoft/onnxscript/blob/main/.lintrunner.toml

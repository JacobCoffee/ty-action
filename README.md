# ty Action

A GitHub Action for running [ty](https://github.com/tusharsadhwani/ty) type checker with automatic GitHub annotations.

## Features

- 🚀 Runs ty type checking on your Python code
- 📝 Automatic GitHub annotations for type errors
- 🎯 Supports custom arguments and working directories
- ⚡ Uses `uvx` for fast, isolated execution
- 🔧 Configurable ty version

## Usage

### Basic

```yaml
- uses: JacobCoffee/ty-action@v1
```

### With custom arguments

```yaml
- uses: JacobCoffee/ty-action@v1
  with:
    args: 'check src tests'
```

### With specific version

```yaml
- uses: JacobCoffee/ty-action@v1
  with:
    version: '0.0.1a26'
    args: 'check'
```

### With working directory

```yaml
- uses: JacobCoffee/ty-action@v1
  with:
    working-directory: './backend'
    args: 'check src'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `version` | Version of ty to install | No | `latest` |
| `args` | Arguments to pass to ty | No | `check` |
| `working-directory` | Working directory for ty | No | `.` |

## Example Workflow

```yaml
name: Type Check

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  type-check:
    name: Type Check with ty
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5

      - name: Set up Python
        uses: actions/setup-python@v6
        with:
          python-version: '3.14'

      - name: Run ty
        uses: JacobCoffee/ty-action@v1
        with:
          args: 'check src'
```

## How It Works

1. Installs `uv` via `astral-sh/setup-uv@v6`
2. Runs ty using `uvx` for isolated execution
3. Parses ty output for errors and warnings
4. Creates GitHub annotations for type issues
5. Returns ty's exit code

## Output Format

The action parses ty output and creates annotations in the format:

- **Error**: Red annotation for type errors
- **Warning**: Yellow annotation for type warnings
- **Notice**: Blue annotation for other messages

## Requirements

- Python project with type hints
- Compatible with ty type checker

## License

MIT

## Author

Jacob Coffee (@JacobCoffee)
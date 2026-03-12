# Setup Node.js from .nvmrc

A reusable composite action that sets up Node.js using the version specified in an `.nvmrc` file.

## Usage

```yaml
steps:
  - uses: actions/checkout@v2
  - name: Setup Node.js from .nvmrc
    uses: ./actions/setup-node-from-nvmrc
```

## Requirements

- The repository must have an `.nvmrc` file in the root directory
- The `.nvmrc` file should contain a valid Node.js version (e.g., `16.14.0`, `18.x`)

## What it does

1. Reads the Node.js version from the `.nvmrc` file
2. Sets up Node.js with the specified version using `actions/setup-node@v2`

## Benefits

- Centralizes Node.js version management in `.nvmrc`
- Eliminates duplicated setup code across workflows
- Uses modern GitHub Actions output syntax (`$GITHUB_OUTPUT`)

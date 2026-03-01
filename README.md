# Build Mark

GitHub Action to build a [Mark](https://github.com/accuser/mark) project with execution caching and artifact upload.

## Usage

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: accuser/setup-mark@v1
  - uses: accuser/build-mark@v1
```

**Note:** Mark must be installed before using this action. Use [`accuser/setup-mark`](https://github.com/accuser/setup-mark) or install Mark manually.

## Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `working-directory` | `.` | Project root directory |
| `cache-execution` | `true` | Cache code execution results between runs |
| `cache-version` | `1` | Cache version prefix (bump to invalidate all caches) |
| `artifact-name` | `mark-build` | Name for the uploaded build artifact |
| `upload-artifact` | `true` | Upload build output as a workflow artifact |

## Execution caching

Projects with executable code blocks benefit from execution caching. The `.mark/cache/` directory is persisted between workflow runs so unchanged code blocks are not re-executed.

The cache key is derived from:

- Content hashes of all Markdown files
- Python version
- A version prefix you control

To force a full rebuild, bump `cache-version`:

```yaml
- uses: accuser/build-mark@v1
  with:
    cache-version: "2"
```

## License

MIT

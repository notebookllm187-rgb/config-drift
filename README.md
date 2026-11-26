# config-drift

A small, dependency-free CLI that checks whether a local `.env` file has drifted from its committed template.

`config-drift` compares variable names only. It never prints, stores, or transmits environment-variable values.

## Why

Teams often update `.env.example` but forget to update their local setup instructions or deployment templates. This leaves developers with missing configuration keys—or stale keys that are no longer used. This tool makes that mismatch visible before an application fails at runtime.

## Requirements

- Python 3.9+
- No third-party dependencies

## Usage

```bash
python -m config_drift --template .env.example --env-file .env
```

Example output:

```text
config-drift: .env is missing 1 key: API_REGION
config-drift: .env has 1 extra key: LEGACY_TOKEN
```

Exit codes:
- `0`: no drift detected
- `1`: missing or extra keys detected
- `2`: input or parsing error

By default, values are ignored. Lines beginning with `#` and blank lines are ignored. Both `export KEY=value` and `KEY=value` are supported.

## Safety

- Only variable names are compared.
- Values are never included in output.
- Files are read locally and are never uploaded.
- Do not commit real `.env` files. Keep them in `.gitignore`.

## Development

```bash
python -m unittest discover -s tests -v
```

## Roadmap

- Optional allowlist for intentionally local-only variables
- CI-friendly GitHub Actions example
- Support for additional dotenv conventions, with tests

## Contributing

Bug reports and focused pull requests are welcome. Please include tests for parser or comparison changes. Never include real secrets in issues, pull requests, fixtures, or screenshots.

## License

MIT. See [LICENSE](LICENSE).

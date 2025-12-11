# afs-cli

> Command-line tool for validating, linting, and formatting Agent Formation files.

⚠️ **Coming soon** — This repo is a placeholder.

---

## Planned Features

### Validate
Schema validation — is it valid AFS?

```bash
afs validate formation.afs
afs validate agents/*.afs --schema agent
afs validate .  # Validate entire formation directory
```

Checks:
- Required fields present
- Correct types
- Valid secret references
- Valid component references
- Schema version compatibility

### Lint
Best practices — is it *good* AFS?

```bash
afs lint formation.afs
afs lint . --fix  # Auto-fix where possible
```

Checks:
- Descriptive IDs (not `agent1`, `mcp-server-2`)
- No unused secret references
- No deprecated fields
- Consistent naming conventions
- Missing descriptions
- Overly permissive defaults

### Format
Auto-format for consistency:

```bash
afs fmt formation.afs
afs fmt . --check  # Check without modifying (for CI)
```

---

## Installation

### Homebrew (macOS/Linux)
```bash
brew install agent-formation/tap/afs
```

### Go
```bash
go install github.com/agent-formation/afs-cli/cmd/afs@latest
```

### Binary releases
Download from [Releases](https://github.com/agent-formation/afs-cli/releases) for:
- Linux (amd64, arm64)
- macOS (amd64, arm64)
- Windows (amd64)

---

## Usage

```bash
# Validate a single file
afs validate formation.afs

# Validate with specific schema type
afs validate agents/support.afs --schema agent

# Lint entire directory
afs lint .

# Format in place
afs fmt .

# Check formatting (CI mode)
afs fmt . --check

# Output as JSON (for integrations)
afs validate . --output json
```

---

## Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Validation/lint errors found |
| 2 | Invalid arguments or file not found |

---

## CI Integration

### GitHub Actions
```yaml
- name: Validate AFS
  run: |
    afs validate .
    afs lint .
    afs fmt . --check
```

---

## Architecture

```
afs-cli/
├── cmd/afs/           # CLI entrypoint
├── pkg/
│   ├── parser/        # AFS/YAML file parsing
│   ├── validator/     # Schema validation engine
│   ├── linter/        # Lint rule engine
│   ├── formatter/     # Auto-formatter
│   └── schema/        # Embedded JSON schemas
├── rules/             # Lint rule definitions
└── testdata/          # Fixtures for testing
```

---

## JSON Schema Export

For external tooling, JSON Schema files are available:

```bash
afs schema export --output ./schemas/
```

Or download directly from releases.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## License

Apache License 2.0

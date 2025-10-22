# Claude Code Instructions for Circuit Breaker Check Buildkite Plugin

## Project Overview
This is a Buildkite plugin that monitors build logs for Circuit Breaker errors and provides helpful guidance to engineers when these issues are detected.

**Tech Stack**: Bash scripting, Buildkite API, AWS

## Code Style Guidelines

### Bash Scripting Standards
- Always start scripts with `#!/bin/bash` shebang
- Use `set -e` for early error detection
- Quote all variables: `"$variable_name"`
- Use lowercase_with_underscores for local variables
- Use UPPERCASE for environment variables
- Use `grep -q` for silent pattern matching

### API Usage
- Use `curl` with proper Authorization headers
- Use backslash continuation for multi-line commands
- Handle API responses appropriately

## Testing & Validation

### Local Testing
```bash
# Make hooks executable
chmod +x hooks/post-command

# Test with environment variables
export BUILDKITE_PIPELINE_SLUG="your-pipeline"
export BUILDKITE_BUILD_NUMBER="123"
export BUILDKITE_JOB_ID="job-id"
export NEW_RELIC_API_KEY="your-api-key"
./hooks/post-command
```

### CI/CD
- Backstage validator runs automatically on non-main branches
- Validates catalog-info.yaml format

## Task Completion Checklist
When completing a task:
1. Ensure proper bash error handling (`set -e`)
2. Verify all variables are quoted
3. Check file permissions on hook scripts
4. Update documentation if needed
5. Validate catalog-info.yaml if modified
6. Test locally if possible

## Project Structure
```
.
├── circuit-breaker-check-plugin.yml  # Plugin configuration
├── hooks/
│   └── post-command                  # Main hook script
├── catalog-info.yaml                 # Backstage metadata
└── .github/workflows/                # CI workflows
```

## Team Context
- **Owner**: sre-enablement team
- **Organization**: Culture Amp
- **Lifecycle**: experimental
- **Purpose**: Help engineers debug Circuit Breaker issues during deployments

## Important Notes
- This is a Buildkite plugin - real testing happens in actual pipelines
- Environment variables come from Buildkite automatically
- The post-command hook runs after the main build command
- API key (NEW_RELIC_API_KEY) must be configured in Buildkite

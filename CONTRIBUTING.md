# Contributing to BTCDecoded Governance

Thank you for your interest in contributing to the BTCDecoded governance system! This document contains repo-specific guidelines. See the [BTCDecoded Contribution Guide](https://github.com/BTCDecoded/.github/blob/main/CONTRIBUTING.md) for general guidelines.

## Code of Conduct

This project follows the [Rust Code of Conduct](https://www.rust-lang.org/policies/code-of-conduct). By participating, you agree to uphold this code.

## How to Contribute

### Reporting Issues

Before creating an issue, please:

1. **Search existing issues** to avoid duplicates
2. **Check the documentation** to ensure it's not a usage question
3. **Review GOVERNANCE.md** to understand the system

For security issues, see [SECURITY.md](SECURITY.md).

### Submitting Pull Requests

1. **Fork the repository**
2. **Create a feature branch** from `main`
3. **Make your changes** following our guidelines
4. **Update documentation** as needed
5. **Submit a pull request**

## Development Guidelines

### Configuration File Changes

The `config/` directory contains YAML configuration files:

- **Follow YAML syntax** - Use proper indentation and formatting
- **Validate schemas** - Ensure configuration matches expected structure
- **Document changes** - Update relevant documentation
- **Test thoroughly** - Verify governance-app can parse changes

### Governance Rule Changes

When modifying governance rules:

- **Review GOVERNANCE.md** - Understand the governance model
- **Consider impact** - Changes affect all repositories
- **Coordinate with maintainers** - Major changes need discussion
- **Follow meta-governance** - Governance changes require special process

### Documentation Changes

- **Keep documentation current** - Update when rules change
- **Cross-reference properly** - Link to related docs
- **Maintain consistency** - Use consistent terminology
- **Examples help** - Add examples for clarity

## Development Setup

### Prerequisites

- Text editor or IDE
- YAML linter (optional but recommended)
- Git

### Validating Configuration

```bash
# Check YAML syntax
yamllint config/*.yml

# Validate with governance-app (if available)
cd ../governance-app
cargo run -- validate-config ../governance/config/
```

## Commit Message Format

Use conventional commits:

```
type(scope): description

[optional body]

[optional footer]
```

**Types:**
- `feat`: New feature or governance rule
- `fix`: Bug fix or rule correction
- `docs`: Documentation changes
- `config`: Configuration changes

**Examples:**
```
feat(tiers): add new tier for security-critical changes
fix(layers): correct layer 1 repository list
docs(guides): update maintainer guide
config(maintainers): add new maintainer key
```

## Review Process

### Pull Request Requirements

- [ ] **Configuration validated** - YAML syntax correct
- [ ] **Documentation updated** - Related docs updated
- [ ] **Impact assessed** - Changes reviewed for effects
- [ ] **Examples provided** - If adding new rules
- [ ] **Cross-references checked** - Links work correctly

### Review Criteria

Reviewers will check:

1. **Correctness** - Are the rules correct?
2. **Consistency** - Do they align with governance model?
3. **Documentation** - Is it clear and complete?
4. **Impact** - What repositories are affected?
5. **Security** - Any security implications?

### Governance Change Process

For changes to governance rules themselves (Tier 5):

1. **Discussion required** - Open discussion first
2. **Consensus building** - Build consensus among maintainers
3. **Special process** - Follow meta-governance procedures
4. **Extended review** - 180-day review period
5. **Economic node input** - Economic nodes may veto

## Getting Help

- **Documentation**: Check GOVERNANCE.md and guides/
- **Issues**: Search existing issues or create new ones
- **Discussions**: Use GitHub Discussions for questions
- **Security**: See [SECURITY.md](SECURITY.md)

## Questions?

If you have questions about contributing, please:

1. **Check this document** first
2. **Review GOVERNANCE.md** for governance model
3. **Search existing issues** for similar questions
4. **Create a new issue** with the "question" label

Thank you for contributing to Bitcoin governance! 🚀


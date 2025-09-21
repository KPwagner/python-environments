# Python Environments

A comprehensive guide to different Python environment and dependency management tools. This repository provides detailed documentation, quick start guides, and best practices for the most popular Python development tools.

## Overview

Managing Python environments and dependencies is crucial for successful Python development. This repository covers four major approaches to Python environment and dependency management:

- **[pyenv + venv](./pyenv-venv/)** - Python version management with built-in virtual environments
- **[Pipenv](./pipenv/)** - High-level tool combining pip and virtualenv functionality  
- **[Poetry](./poetry/)** - Modern dependency management and packaging tool
- **[uv](./uv/)** - Ultra-fast Python package installer and resolver

## Tool Comparison

| Feature | pyenv + venv | Pipenv | Poetry | uv |
|---------|-------------|--------|--------|-----|
| **Python Version Management** | ✅ (pyenv) | ❌ | ❌ | ✅ |
| **Virtual Environment** | ✅ (venv) | ✅ | ✅ | ✅ |
| **Dependency Resolution** | Basic (pip) | Advanced | Advanced | Advanced |
| **Lock Files** | ❌ | ✅ (Pipfile.lock) | ✅ (poetry.lock) | ✅ (uv.lock) |
| **Package Building** | Manual | ❌ | ✅ | ✅ |
| **Performance** | Standard | Standard | Standard | ⚡ Ultra-fast |
| **Configuration File** | requirements.txt | Pipfile | pyproject.toml | pyproject.toml |
| **Learning Curve** | Low | Medium | Medium | Low-Medium |
| **Ecosystem Maturity** | Very High | High | High | Growing |

## Getting Started

### Choose Your Tool

**Use pyenv + venv if:**
- You need maximum compatibility with existing projects
- You prefer simple, well-established tools
- You want fine-grained control over Python versions
- You're working with legacy codebases

**Use Pipenv if:**
- You want automatic virtual environment management
- You need advanced dependency resolution
- You're migrating from requirements.txt workflows
- You want built-in security scanning

**Use Poetry if:**
- You're building packages for distribution
- You want modern Python packaging standards
- You need sophisticated dependency management
- You prefer declarative configuration

**Use uv if:**
- You prioritize speed and performance
- You want modern tooling with pip compatibility
- You're starting new projects
- You need fast CI/CD pipelines

### Quick Installation Links

- **pyenv**: [Installation Guide](./pyenv-venv/README.md#installation)
- **Pipenv**: [Installation Guide](./pipenv/README.md#installation)  
- **Poetry**: [Installation Guide](./poetry/README.md#installation)
- **uv**: [Installation Guide](./uv/README.md#installation)

## Common Workflows

### Starting a New Project

#### pyenv + venv
```bash
pyenv local 3.11.0
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

#### Pipenv
```bash
pipenv --python 3.11
pipenv install requests
pipenv shell
```

#### Poetry
```bash
poetry new my-project
cd my-project
poetry add requests
poetry shell
```

#### uv
```bash
uv init my-project
cd my-project  
uv add requests
uv sync
```

### Working on Existing Projects

Each tool provides commands to quickly set up development environments for existing projects. See the individual tool documentation for detailed workflows.

## Best Practices

### Universal Best Practices

1. **Always use virtual environments** for project isolation
2. **Pin dependencies** with version constraints
3. **Use lock files** for reproducible builds (when available)
4. **Keep dependency lists updated** and remove unused packages
5. **Separate development and production dependencies**
6. **Document your chosen tool** in project README files
7. **Use `.gitignore`** to exclude virtual environments and cache directories

### Tool-Specific Guidelines

Each tool has its own set of best practices and conventions. Refer to the individual documentation pages for detailed guidance:

- [pyenv + venv Best Practices](./pyenv-venv/README.md#best-practices)
- [Pipenv Best Practices](./pipenv/README.md#best-practices)
- [Poetry Best Practices](./poetry/README.md#best-practices)
- [uv Best Practices](./uv/README.md#best-practices)

## Migration Guides

Moving between tools is possible, though each transition has its own considerations:

- **From requirements.txt** → See migration sections in Pipenv, Poetry, or uv docs
- **From Pipenv to Poetry** → Convert Pipfile to pyproject.toml format
- **From Poetry to uv** → Adapt pyproject.toml structure for uv compatibility
- **Between any tools** → Export/import requirements.txt as intermediate format

## Contributing

This repository welcomes contributions! Please feel free to:

- Submit issues for corrections or improvements
- Add new sections or tools
- Improve existing documentation
- Share your experiences and best practices

## Additional Resources

### General Python Packaging
- [Python Packaging User Guide](https://packaging.python.org/) - Official packaging documentation
- [PEP 518](https://www.python.org/dev/peps/pep-0518/) - pyproject.toml specification
- [Python Virtual Environments Primer](https://realpython.com/python-virtual-environments-a-primer/)

### Community
- [r/Python](https://www.reddit.com/r/Python/) - Python community discussions
- [Python Discord](https://discord.gg/python) - Real-time community support
- [Python Package Index (PyPI)](https://pypi.org/) - Python package repository

---

**Quick Navigation:**
- [pyenv + venv Documentation](./pyenv-venv/) 
- [Pipenv Documentation](./pipenv/)
- [Poetry Documentation](./poetry/)
- [uv Documentation](./uv/)

# Poetry

## Overview

**Poetry** is a modern dependency management and packaging tool for Python that aims to simplify project management through a single configuration file. It provides sophisticated dependency resolution, virtual environment management, and package building capabilities.

### Tool Description

Poetry combines dependency management, virtual environment handling, and package building into a unified workflow. It uses the `pyproject.toml` file (following PEP 518) as the single source of truth for project configuration, dependencies, and metadata. Poetry's dependency resolver is more robust than pip's, handling complex dependency trees with better conflict resolution.

### Core Capabilities

- **Advanced Dependency Resolution**: Sophisticated solver for complex dependency graphs
- **Virtual Environment Management**: Automatic creation and management of isolated environments
- **Package Building and Publishing**: Built-in support for building and publishing to PyPI
- **Lock File Management**: Deterministic dependency installation with poetry.lock
- **Project Scaffolding**: Generate new projects with proper structure
- **Development vs Production Dependencies**: Clean separation of dependency groups
- **Version Management**: Semantic versioning support and automated version bumping
- **Plugin System**: Extensible through plugins for additional functionality

## Quick Start Guide

### Installation

#### Using the official installer (recommended)
```bash
curl -sSL https://install.python-poetry.org | python3 -
```

#### Using pip
```bash
pip install poetry
```

#### Using Homebrew (macOS)
```bash
brew install poetry
```

### Configure Poetry (optional but recommended)
```bash
# Configure Poetry to create virtual environments in project directory
poetry config virtualenvs.in-project true

# Check current configuration
poetry config --list
```

### Basic Usage

#### 1. Create a new project
```bash
# Create new project with directory structure
poetry new my-awesome-project

# Or initialize Poetry in existing directory
cd existing-project
poetry init
```

#### 2. Install dependencies
```bash
# Install all dependencies from pyproject.toml
poetry install

# Add a new dependency
poetry add requests

# Add development dependency
poetry add pytest --group dev

# Add optional dependency group
poetry add sphinx --group docs
```

#### 3. Manage virtual environment
```bash
# Activate the virtual environment
poetry shell

# Run commands in the virtual environment
poetry run python script.py
poetry run pytest

# Show virtual environment info
poetry env info

# Exit shell
exit
```

#### 4. Dependency management
```bash
# Update dependencies
poetry update

# Update specific package
poetry update requests

# Remove a dependency
poetry remove requests

# Show dependency tree
poetry show --tree

# Check for outdated packages
poetry show --outdated
```

### Project Structure

A typical Poetry project structure:
```
my-awesome-project/
├── pyproject.toml      # Project configuration and dependencies
├── poetry.lock         # Locked dependency versions
├── README.md
├── my_awesome_project/
│   └── __init__.py
└── tests/
    └── __init__.py
```

### pyproject.toml Example

```toml
[tool.poetry]
name = "my-awesome-project"
version = "0.1.0"
description = "A sample Python project"
authors = ["Your Name <you@example.com>"]
readme = "README.md"
packages = [{include = "my_awesome_project"}]

[tool.poetry.dependencies]
python = "^3.8"
requests = "^2.28.0"
click = "^8.0.0"

[tool.poetry.group.dev.dependencies]
pytest = "^7.0.0"
black = "^22.0.0"
flake8 = "^5.0.0"
mypy = "^0.991"

[tool.poetry.group.docs.dependencies]
sphinx = "^5.0.0"
sphinx-rtd-theme = "^1.0.0"

[tool.poetry.scripts]
my-script = "my_awesome_project.main:cli"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"

[tool.black]
line-length = 88
target-version = ['py38']

[tool.mypy]
python_version = "3.8"
warn_return_any = true
warn_unused_configs = true
```

### Dependency Groups

Poetry supports organizing dependencies into groups:

```bash
# Install all groups
poetry install

# Install only main dependencies
poetry install --only main

# Install main + specific groups
poetry install --with dev,docs

# Exclude specific groups
poetry install --without docs

# Install only specific groups
poetry install --only dev
```

### Version Management

```bash
# Show current version
poetry version

# Bump version
poetry version patch    # 0.1.0 -> 0.1.1
poetry version minor    # 0.1.1 -> 0.2.0
poetry version major    # 0.2.0 -> 1.0.0

# Set specific version
poetry version 2.0.0

# Use pre-release versions
poetry version prerelease  # 1.0.0 -> 1.0.1a0
```

### Building and Publishing

```bash
# Build package (creates dist/ directory)
poetry build

# Publish to PyPI (requires authentication)
poetry publish

# Build and publish in one command
poetry publish --build

# Publish to test PyPI
poetry config repositories.testpypi https://test.pypi.org/legacy/
poetry publish -r testpypi
```

### Working with Environments

```bash
# List environments
poetry env list

# Create environment with specific Python version
poetry env use python3.11

# Remove current environment
poetry env remove python

# Show environment path
poetry env info --path

# Run command in environment
poetry run python -c "import sys; print(sys.executable)"
```

### Advanced Features

#### Scripts and Commands
Define custom scripts in pyproject.toml:
```toml
[tool.poetry.scripts]
my-cli = "my_package.cli:main"
dev-server = "my_package.server:run_dev"
```

#### Plugins
```bash
# Install Poetry plugins
poetry self add poetry-plugin-export

# Export requirements.txt
poetry export -f requirements.txt --output requirements.txt

# Export dev requirements
poetry export -f requirements.txt --with dev --output requirements-dev.txt
```

#### Private Repositories
```bash
# Add private repository
poetry source add private https://private-pypi.example.com/simple/

# Configure authentication
poetry config http-basic.private username password

# Install from private repository
poetry add my-private-package --source private
```

### Best Practices

1. **Always commit pyproject.toml and poetry.lock** to version control
2. **Use dependency groups** to organize different types of dependencies
3. **Pin Python version ranges** appropriately in pyproject.toml
4. **Use semantic versioning** for your package versions
5. **Configure Poetry globally** for consistent behavior across projects
6. **Use `poetry install --sync`** in CI/CD to ensure exact environment reproduction
7. **Regularly update dependencies** with `poetry update`
8. **Use `poetry check`** to validate pyproject.toml format

### Common Commands Reference

```bash
# Project management
poetry new project-name          # Create new project
poetry init                      # Initialize existing project
poetry install                   # Install dependencies
poetry install --sync            # Install and remove to match lock file exactly

# Dependency management
poetry add package               # Add dependency
poetry add package --group dev   # Add to dev group
poetry remove package            # Remove dependency
poetry update                    # Update all dependencies
poetry update package           # Update specific package
poetry show                     # List installed packages
poetry show --tree              # Show dependency tree
poetry show package             # Show package details

# Environment management
poetry shell                    # Activate virtual environment
poetry run command              # Run command in environment
poetry env info                 # Show environment info
poetry env list                 # List environments
poetry env use python3.11       # Use specific Python version

# Building and publishing
poetry build                    # Build package
poetry publish                  # Publish to PyPI
poetry version                  # Show/set version
poetry check                    # Validate pyproject.toml

# Configuration
poetry config --list            # Show configuration
poetry config setting value     # Set configuration
```

### Migration from Other Tools

#### From requirements.txt
```bash
# Install poetry in existing project
poetry init

# Add dependencies interactively or manually edit pyproject.toml
# Install to create lock file
poetry install
```

#### From pipenv
```bash
# Convert Pipfile to pyproject.toml
poetry init

# Manually add dependencies from Pipfile
# Or use poetry-pipfile-migrate plugin
```

### Troubleshooting

#### Common Issues

**Lock file conflicts:**
```bash
poetry lock --no-update  # Regenerate lock without updating
```

**Cache issues:**
```bash
poetry cache clear --all pypi  # Clear package cache
```

**Environment issues:**
```bash
poetry env remove python  # Remove and recreate environment
poetry install
```

**Authentication issues:**
```bash
poetry config --list  # Check stored credentials
poetry config http-basic.pypi username password
```

## External Resources

### Official Documentation
- [Poetry Official Documentation](https://python-poetry.org/docs/) - Comprehensive documentation and user guide
- [Poetry GitHub Repository](https://github.com/python-poetry/poetry) - Source code and issue tracking
- [PEP 517](https://www.python.org/dev/peps/pep-0517/) - Build system interface specification
- [PEP 518](https://www.python.org/dev/peps/pep-0518/) - pyproject.toml specification

### Tutorials and Guides
- [Real Python - Poetry Guide](https://realpython.com/dependency-management-python-poetry/) - Comprehensive Poetry tutorial
- [Poetry vs pip vs pipenv](https://python-poetry.org/docs/basic-usage/) - Official comparison guide
- [Modern Python packaging with Poetry](https://hackersandslackers.com/python-poetry-package-manager/) - Practical guide

### Configuration and Best Practices
- [Poetry Configuration](https://python-poetry.org/docs/configuration/) - Complete configuration reference
- [Dependency specification](https://python-poetry.org/docs/dependency-specification/) - Advanced dependency management
- [Managing environments](https://python-poetry.org/docs/managing-environments/) - Virtual environment best practices

### Tools and Integrations
- [Poetry Plugins](https://python-poetry.org/docs/plugins/) - Available plugins and extensions
- [VS Code Poetry Extension](https://marketplace.visualstudio.com/items?itemName=zeshuaro.vscode-python-poetry) - IDE integration
- [Docker with Poetry](https://python-poetry.org/docs/master/faq/#i-am-on-windows-running-python-on-windows-subsystem-for-linux-and-/or-docker-why-is-poetry-failing) - Containerization guides

### Community Resources
- [Poetry Discussions](https://github.com/python-poetry/poetry/discussions) - Official community discussions
- [Stack Overflow - python-poetry tag](https://stackoverflow.com/questions/tagged/python-poetry) - Community Q&A
- [r/Python Poetry discussions](https://www.reddit.com/r/Python/search/?q=poetry) - Community discussions
- [Poetry Discord](https://discord.gg/awxPgve) - Real-time community support
# uv

## Overview

**uv** is an extremely fast Python package installer and resolver, designed as a drop-in replacement for pip and pip-tools. Built in Rust, uv provides significant performance improvements while maintaining compatibility with the existing Python packaging ecosystem.

### Tool Description

uv is developed by Astral (creators of Ruff) and aims to be a comprehensive Python project management tool. It handles package installation, dependency resolution, virtual environment management, and project scaffolding with unprecedented speed. uv is designed to be compatible with existing Python packaging standards while providing modern features and exceptional performance.

### Core Capabilities

- **Lightning-fast Package Installation**: 10-100x faster than pip for most operations
- **Advanced Dependency Resolution**: Robust resolver with comprehensive conflict detection
- **Virtual Environment Management**: Fast virtual environment creation and management
- **Project Management**: Complete project lifecycle support with uv.lock files
- **Cross-platform Compatibility**: Works seamlessly on Windows, macOS, and Linux
- **pip Compatibility**: Drop-in replacement for most pip commands
- **Modern Python Support**: Full support for Python 3.8+ with upcoming features
- **Workspace Support**: Multi-package project management

## Quick Start Guide

### Installation

#### Using the official installer (recommended)
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

#### Using pip
```bash
pip install uv
```

#### Using Homebrew (macOS)
```bash
brew install uv
```

#### Using Chocolatey (Windows)
```bash
choco install uv
```

#### Using winget (Windows)
```bash
winget install --id=astral-sh.uv  -e
```

### Basic Usage

#### 1. Create a new project
```bash
# Create new project
uv init my-awesome-project
cd my-awesome-project

# Or initialize in existing directory
cd existing-project
uv init
```

#### 2. Virtual environment management
```bash
# Create virtual environment
uv venv

# Activate virtual environment
# On Linux/macOS:
source .venv/bin/activate
# On Windows:
.venv\Scripts\activate

# Create with specific Python version
uv venv --python 3.11

# Create in custom location
uv venv my-env
```

#### 3. Package installation
```bash
# Install packages (much faster than pip)
uv pip install requests

# Install from requirements.txt
uv pip install -r requirements.txt

# Install in development mode
uv pip install -e .

# Install with constraints
uv pip install --constraint constraints.txt requests
```

#### 4. Project dependencies
```bash
# Add dependency to project
uv add requests

# Add development dependency
uv add pytest --dev

# Add optional dependency
uv add sphinx --optional docs

# Install project dependencies
uv sync

# Install only production dependencies
uv sync --no-dev
```

### Project Structure

A typical uv project structure:
```
my-awesome-project/
├── pyproject.toml      # Project configuration
├── uv.lock            # Locked dependency versions
├── .venv/              # Virtual environment (if created in project)
├── src/
│   └── my_awesome_project/
│       └── __init__.py
└── tests/
    └── __init__.py
```

### pyproject.toml Example

```toml
[project]
name = "my-awesome-project"
version = "0.1.0"
description = "A sample Python project"
authors = [
    {name = "Your Name", email = "you@example.com"}
]
readme = "README.md"
requires-python = ">=3.8"
dependencies = [
    "requests>=2.28.0",
    "click>=8.0.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.0.0",
    "black>=22.0.0",
    "ruff>=0.1.0",
]
docs = [
    "sphinx>=5.0.0",
    "sphinx-rtd-theme>=1.0.0",
]

[project.scripts]
my-script = "my_awesome_project.main:cli"

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[tool.uv]
dev-dependencies = [
    "pytest>=7.0.0",
    "black>=22.0.0",
    "ruff>=0.1.0",
]

[tool.ruff]
line-length = 88
target-version = "py38"
```

### Advanced Package Installation

```bash
# Install from Git repository
uv pip install git+https://github.com/user/repo.git

# Install from specific branch/tag/commit
uv pip install git+https://github.com/user/repo.git@main
uv pip install git+https://github.com/user/repo.git@v1.0.0
uv pip install git+https://github.com/user/repo.git@abc123

# Install from local path
uv pip install ./local-package
uv pip install -e ./local-package  # Editable install

# Install with specific index
uv pip install --index-url https://pypi.org/simple/ requests

# Install with extra index
uv pip install --extra-index-url https://private.pypi.org/simple/ requests
```

### Dependency Resolution and Lock Files

```bash
# Generate lock file
uv lock

# Install from lock file
uv sync

# Update specific package
uv lock --upgrade-package requests

# Update all packages
uv lock --upgrade

# Show what would be updated
uv lock --dry-run --upgrade
```

### Working with Requirements Files

```bash
# Generate requirements.txt
uv pip freeze > requirements.txt

# Install from requirements with faster resolution
uv pip install -r requirements.txt

# Compile requirements.txt from pyproject.toml
uv pip compile pyproject.toml -o requirements.txt

# Sync environment with requirements
uv pip sync requirements.txt
```

### Virtual Environment Management

```bash
# List available Python versions
uv python list

# Install specific Python version
uv python install 3.11

# Create venv with specific Python
uv venv --python 3.11.5

# Use specific Python interpreter
uv venv --python /usr/bin/python3.11

# Remove virtual environment
rm -rf .venv  # or just delete the directory

# Show virtual environment info
uv venv --show-path
```

### Tool Running

```bash
# Run tools without installing globally
uv tool run ruff check .
uv tool run black .
uv tool run pytest

# Install tools globally
uv tool install ruff
uv tool install black

# List installed tools
uv tool list

# Upgrade tool
uv tool upgrade ruff

# Uninstall tool
uv tool uninstall ruff
```

### Multi-package Workspaces

Create a `pyproject.toml` with workspace configuration:
```toml
[tool.uv.workspace]
members = ["packages/*"]

[tool.uv.sources]
my-local-package = { workspace = true }
```

```bash
# Sync all workspace packages
uv sync

# Add dependency to specific workspace member
uv add --package my-package requests
```

### Performance and Caching

```bash
# Show cache information
uv cache info

# Clean cache
uv cache clean

# Prune old cache entries
uv cache prune

# Set cache directory
export UV_CACHE_DIR=/custom/cache/path
```

### Best Practices

1. **Use uv for all package operations** instead of pip for better performance
2. **Commit uv.lock files** to ensure reproducible environments
3. **Use virtual environments** for project isolation
4. **Pin Python versions** in pyproject.toml for consistency
5. **Use uv sync** in CI/CD for faster, deterministic builds
6. **Leverage uv tool run** for one-off tool usage
7. **Organize dependencies** using optional-dependencies groups
8. **Use uv python install** to manage Python versions

### Migration from Other Tools

#### From pip + venv
```bash
# Replace pip commands with uv pip
pip install requests        → uv pip install requests
pip install -r requirements.txt → uv pip install -r requirements.txt
pip freeze > requirements.txt   → uv pip freeze > requirements.txt

# Virtual environment creation
python -m venv .venv       → uv venv
```

#### From Poetry
```bash
# Convert Poetry project
# 1. Copy dependencies from pyproject.toml [tool.poetry.dependencies]
#    to [project.dependencies]
# 2. Convert dev dependencies to [tool.uv.dev-dependencies]
# 3. Run uv sync to create uv.lock
```

#### From Pipenv
```bash
# Convert Pipfile to pyproject.toml dependencies
# Then use uv to manage the project
uv init
# Add dependencies manually or from Pipfile
uv add requests flask
uv add pytest --dev
```

### Common Commands Reference

```bash
# Project management
uv init [path]                   # Initialize new project
uv add package                   # Add dependency
uv add package --dev             # Add dev dependency
uv remove package                # Remove dependency
uv sync                          # Install all dependencies from lock
uv sync --no-dev                 # Install only production dependencies
uv lock                          # Generate/update lock file

# Package installation (pip-compatible)
uv pip install package           # Install package
uv pip install -r requirements.txt # Install from requirements
uv pip install -e .              # Editable install
uv pip uninstall package         # Remove package
uv pip freeze                    # List installed packages
uv pip list                      # List installed packages (formatted)
uv pip show package              # Show package information

# Virtual environments
uv venv [path]                   # Create virtual environment
uv venv --python 3.11            # Create with specific Python version

# Python version management
uv python list                   # List available Python versions
uv python install 3.11          # Install Python version

# Tools
uv tool run command              # Run tool without installing
uv tool install tool             # Install tool globally
uv tool list                     # List installed tools
uv tool upgrade tool             # Upgrade tool
uv tool uninstall tool           # Uninstall tool

# Cache management
uv cache clean                   # Clean cache
uv cache info                    # Show cache info
```

### Troubleshooting

#### Common Issues

**Performance not as expected:**
```bash
# Check if using system pip instead of uv
which pip  # Should not be uv pip for direct usage
uv pip install package  # Use uv pip explicitly
```

**Virtual environment issues:**
```bash
# Recreate virtual environment
rm -rf .venv
uv venv
uv sync
```

**Lock file conflicts:**
```bash
# Regenerate lock file
rm uv.lock
uv lock
```

**Python version issues:**
```bash
# Check available Python versions
uv python list

# Install required Python version
uv python install 3.11
```

## External Resources

### Official Documentation
- [uv Official Documentation](https://docs.astral.sh/uv/) - Comprehensive documentation and user guide
- [uv GitHub Repository](https://github.com/astral-sh/uv) - Source code and issue tracking
- [uv Blog Posts](https://astral.sh/blog/uv) - Updates and announcements from the Astral team

### Tutorials and Guides
- [uv: Python packaging in Rust](https://astral.sh/blog/uv) - Introduction blog post
- [Modern Python packaging with uv](https://hynek.me/articles/python-uv/) - Practical guide by Hynek Schlawack
- [Migrating from Poetry to uv](https://docs.astral.sh/uv/guides/projects/) - Migration guide

### Performance and Benchmarks
- [uv Performance Benchmarks](https://astral.sh/blog/uv#performance) - Official performance comparisons
- [Python Package Installation Speed](https://blog.pythonspeed.com/2024/01/faster-python-package-installs/) - Independent benchmarks
- [uv vs pip vs Poetry](https://packaging.python.org/en/latest/key_projects/#uv) - Packaging authority comparison

### Integration and Tooling
- [GitHub Actions with uv](https://docs.astral.sh/uv/guides/integration/github/) - CI/CD integration
- [Docker with uv](https://docs.astral.sh/uv/guides/integration/docker/) - Containerization
- [VS Code integration](https://docs.astral.sh/uv/guides/integration/editor/) - Editor support

### Community Resources
- [uv Discussions](https://github.com/astral-sh/uv/discussions) - Official community discussions
- [Stack Overflow - uv tag](https://stackoverflow.com/questions/tagged/uv) - Community Q&A
- [r/Python uv discussions](https://www.reddit.com/r/Python/search/?q=uv) - Community discussions
- [Astral Discord](https://discord.gg/astral-sh) - Real-time community support
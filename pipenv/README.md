# Pipenv

## Overview

**Pipenv** is a powerful tool that combines package management and virtual environment creation for Python projects. It aims to bring the best of all packaging worlds to the Python world by combining pip and virtualenv functionality.

### Tool Description

Pipenv automatically creates and manages virtual environments for your Python projects, while also providing advanced dependency resolution and package installation capabilities. It uses `Pipfile` and `Pipfile.lock` to manage dependencies, making dependency management more deterministic and secure than traditional `requirements.txt` files.

### Core Capabilities

- **Automatic Virtual Environment Management**: Creates and manages virtual environments automatically
- **Advanced Dependency Resolution**: Handles complex dependency trees and conflicts
- **Security Scanning**: Built-in security vulnerability scanning for installed packages
- **Deterministic Builds**: Lock files ensure reproducible installations across environments
- **Development vs Production Dependencies**: Separate dependency groups for different environments
- **Environment Variable Management**: Built-in support for `.env` files
- **Graph Visualization**: Dependency graph visualization and analysis

## Quick Start Guide

### Installation

#### Using pip
```bash
pip install pipenv
```

#### Using Homebrew (macOS)
```bash
brew install pipenv
```

#### Using apt (Ubuntu/Debian)
```bash
sudo apt install pipenv
```

### Basic Usage

#### 1. Initialize a new project
```bash
# Navigate to your project directory
cd my-python-project

# Initialize pipenv (creates Pipfile)
pipenv --python 3.11

# Or use system Python version
pipenv install
```

#### 2. Install packages
```bash
# Install a package (adds to Pipfile and installs in virtual environment)
pipenv install requests

# Install development dependencies
pipenv install pytest --dev

# Install from Pipfile
pipenv install

# Install from Pipfile.lock (exact versions)
pipenv install --deploy
```

#### 3. Activate and use the virtual environment
```bash
# Activate the virtual environment
pipenv shell

# Run commands in the virtual environment without activating
pipenv run python script.py
pipenv run pytest

# Exit the virtual environment
exit
```

#### 4. Managing dependencies
```bash
# Show dependency graph
pipenv graph

# Check for security vulnerabilities
pipenv check

# Update packages
pipenv update

# Update specific package
pipenv update requests

# Remove a package
pipenv uninstall requests
```

### Project Structure

A typical pipenv project structure:
```
my-project/
├── Pipfile          # Project dependencies and settings
├── Pipfile.lock     # Locked dependency versions (generated)
├── .env             # Environment variables (optional)
├── src/
│   └── main.py
└── tests/
    └── test_main.py
```

### Pipfile Example

```toml
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]
requests = "*"
flask = ">=2.0.0"
click = "~=8.0"

[dev-packages]
pytest = "*"
black = "*"
flake8 = "*"

[requires]
python_version = "3.11"

[scripts]
test = "pytest"
format = "black ."
lint = "flake8 ."
```

### Environment Variables

Create a `.env` file in your project root:
```env
DATABASE_URL=postgresql://localhost/mydb
SECRET_KEY=your-secret-key-here
DEBUG=True
```

Pipenv automatically loads these variables when you run `pipenv shell` or `pipenv run`.

### Common Workflows

#### Starting a new project
```bash
mkdir my-project && cd my-project
pipenv --python 3.11
pipenv install flask requests
pipenv install pytest black --dev
pipenv shell
```

#### Working on an existing project
```bash
git clone <repository>
cd <project-directory>
pipenv install --dev
pipenv shell
```

#### Production deployment
```bash
# Install only production dependencies
pipenv install --deploy --ignore-pipfile

# Or use pip with generated requirements
pipenv requirements > requirements.txt
pip install -r requirements.txt
```

### Advanced Features

#### Custom Scripts
Add custom scripts to your Pipfile:
```toml
[scripts]
dev = "python app.py"
test = "pytest -v"
deploy = "python deploy.py"
```

Run with:
```bash
pipenv run dev
pipenv run test
pipenv run deploy
```

#### Environment-specific Dependencies
```bash
# Install for specific environments
pipenv install --dev pytest
pipenv install --pre django  # Install pre-release versions
```

#### Dependency Specification
```toml
[packages]
requests = "*"              # Any version
django = ">=3.0"           # Minimum version
flask = "~=2.0.0"          # Compatible release
numpy = "==1.21.0"         # Exact version
```

### Best Practices

1. **Always commit Pipfile and Pipfile.lock** to version control
2. **Use `--deploy` flag in production** for exact dependency installation
3. **Separate development and production dependencies** using `--dev` flag
4. **Use environment variables** for configuration instead of hardcoding
5. **Regularly run `pipenv check`** to scan for security vulnerabilities
6. **Use meaningful script names** in your Pipfile for common tasks
7. **Don't commit `.env` files** with sensitive information

### Common Commands Reference

```bash
pipenv install                    # Install dependencies from Pipfile
pipenv install package           # Install a package
pipenv install package --dev     # Install development dependency
pipenv install --deploy          # Install from Pipfile.lock exactly
pipenv uninstall package         # Remove a package
pipenv shell                      # Activate virtual environment
pipenv run command               # Run command in virtual environment
pipenv graph                     # Show dependency graph
pipenv check                     # Check for security vulnerabilities
pipenv update                    # Update all packages
pipenv update package           # Update specific package
pipenv --venv                    # Show virtual environment path
pipenv --where                   # Show project directory
pipenv clean                     # Remove packages not in Pipfile
pipenv requirements             # Generate requirements.txt output
pipenv lock                     # Generate Pipfile.lock
```

### Troubleshooting

#### Common Issues and Solutions

**Virtual environment location:**
```bash
# Find virtual environment location
pipenv --venv

# Set custom virtual environment location
export PIPENV_VENV_IN_PROJECT=1  # Creates .venv in project directory
```

**Clear cache:**
```bash
pipenv --clear  # Clear cache and create new virtual environment
```

**Fix lock file issues:**
```bash
pipenv lock --clear  # Clear lock file and regenerate
```

## External Resources

### Official Documentation
- [Pipenv Official Documentation](https://pipenv.pypa.io/) - Complete documentation and user guide
- [Pipenv GitHub Repository](https://github.com/pypa/pipenv) - Source code and issue tracking
- [PEP 508](https://www.python.org/dev/peps/pep-0508/) - Dependency specification format used by Pipenv

### Tutorials and Guides
- [Real Python - Pipenv Guide](https://realpython.com/pipenv-guide/) - Comprehensive tutorial on Pipenv
- [Python.org - Managing Application Dependencies](https://packaging.python.org/tutorials/managing-dependencies/) - Official Python packaging guide
- [Pipenv vs pip vs conda](https://towardsdatascience.com/pipenv-vs-pip-vs-conda-8f8f7ac1df06) - Comparison of Python package managers

### Best Practices and Articles
- [Pipenv Best Practices](https://docs.pipenv.org/en/latest/advanced/) - Advanced usage patterns
- [Python Application Dependency Management](https://hynek.me/articles/python-app-deps-2018/) - Modern dependency management approaches
- [Secure Python Dependencies](https://python-security.readthedocs.io/dependencies.html) - Security considerations

### Tools and Integrations
- [Pipenv in Docker](https://hub.docker.com/_/python) - Using Pipenv with Docker containers
- [VS Code Python Extension](https://code.visualstudio.com/docs/python/environments) - IDE integration
- [PyCharm Pipenv Support](https://www.jetbrains.com/help/pycharm/pipenv.html) - JetBrains IDE integration

### Community Resources
- [Stack Overflow - pipenv tag](https://stackoverflow.com/questions/tagged/pipenv) - Community Q&A
- [r/Python pipenv discussions](https://www.reddit.com/r/Python/search/?q=pipenv) - Community discussions
- [Python Discord](https://discord.gg/python) - Real-time community support
# Pyenv + Venv

## Overview

This guide covers using **pyenv** and **venv** together for Python environment and dependency management. This combination provides excellent version control and virtual environment isolation for Python projects.

### Tools Description

**pyenv** is a Python version management tool that allows you to easily install, switch between, and manage multiple Python versions on your system. It works by intercepting Python commands using shims and determining which Python version to run based on your configuration.

**venv** is Python's built-in module for creating virtual environments. It creates isolated Python environments with their own site-packages directories, allowing you to install packages without affecting the global Python installation.

### Core Capabilities

- **Python Version Management**: Install and switch between multiple Python versions
- **Project-specific Python versions**: Set different Python versions for different projects
- **Virtual Environment Isolation**: Create isolated environments for each project
- **Dependency Management**: Install packages in isolated environments
- **No conflicts**: Avoid package version conflicts between projects
- **Built-in support**: venv comes with Python 3.3+ (no additional installation needed)

## Quick Start Guide

### Installation

#### Installing pyenv

**macOS (using Homebrew):**
```bash
brew install pyenv
```

**Linux/macOS (using pyenv-installer):**
```bash
curl https://pyenv.run | bash
```

**Manual installation:**
```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

Add pyenv to your shell configuration:
```bash
# Add to ~/.bashrc, ~/.zshrc, or ~/.bash_profile
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

#### venv Setup
venv comes built-in with Python 3.3+, so no separate installation is needed.

### Basic Usage

#### 1. Install and set Python version with pyenv
```bash
# List available Python versions
pyenv install --list

# Install a specific Python version
pyenv install 3.11.0

# Set global Python version
pyenv global 3.11.0

# Set local Python version for current project
pyenv local 3.11.0

# Check current Python version
python --version
```

#### 2. Create and manage virtual environments with venv
```bash
# Create a new virtual environment
python -m venv myproject-env

# Activate the virtual environment
# On Linux/macOS:
source myproject-env/bin/activate
# On Windows:
myproject-env\Scripts\activate

# Verify activation (should show the venv path)
which python

# Install packages
pip install requests flask

# Generate requirements file
pip freeze > requirements.txt

# Deactivate virtual environment
deactivate
```

#### 3. Complete project setup workflow
```bash
# Navigate to your project directory
cd my-python-project

# Set Python version for this project
pyenv local 3.11.0

# Create virtual environment
python -m venv .venv

# Activate virtual environment
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Start working on your project
python main.py
```

### Managing Dependencies

#### Creating requirements.txt
```bash
# After installing packages in your virtual environment
pip freeze > requirements.txt
```

#### Installing from requirements.txt
```bash
# In a new environment
pip install -r requirements.txt
```

#### Example requirements.txt
```
requests==2.31.0
flask==2.3.2
pytest==7.4.0
black==23.3.0
```

### Best Practices

1. **Always use virtual environments** for each project
2. **Use pyenv local** to set project-specific Python versions
3. **Keep requirements.txt updated** with your dependencies
4. **Use descriptive names** for virtual environments
5. **Activate environments** before working on projects
6. **Don't commit virtual environments** to version control (add to .gitignore)

### Common Commands Reference

#### pyenv commands
```bash
pyenv versions                 # List installed Python versions
pyenv version                  # Show current Python version
pyenv install 3.11.0          # Install Python 3.11.0
pyenv uninstall 3.11.0        # Uninstall Python 3.11.0
pyenv global 3.11.0           # Set global Python version
pyenv local 3.11.0            # Set local Python version
pyenv shell 3.11.0            # Set shell Python version
```

#### venv commands
```bash
python -m venv env_name        # Create virtual environment
source env_name/bin/activate   # Activate (Linux/macOS)
env_name\Scripts\activate      # Activate (Windows)
deactivate                     # Deactivate environment
pip freeze                     # List installed packages
pip freeze > requirements.txt  # Export dependencies
pip install -r requirements.txt # Install dependencies
```

## External Resources

### Official Documentation
- [pyenv GitHub Repository](https://github.com/pyenv/pyenv) - Official pyenv repository with installation and usage instructions
- [Python venv Documentation](https://docs.python.org/3/library/venv.html) - Official Python documentation for venv
- [Python Virtual Environments Guide](https://docs.python.org/3/tutorial/venv.html) - Python.org tutorial on virtual environments

### Tutorials and Guides
- [Real Python - Python Virtual Environments Guide](https://realpython.com/python-virtual-environments-a-primer/) - Comprehensive guide to Python virtual environments
- [Real Python - pyenv Guide](https://realpython.com/intro-to-pyenv/) - Detailed introduction to pyenv
- [Python Guide - Virtual Environments](https://docs.python-guide.org/dev/virtualenvs/) - Best practices for virtual environments

### Tools and Utilities
- [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv) - pyenv plugin for managing virtualenv environments
- [pyenv-installer](https://github.com/pyenv/pyenv-installer) - Automatic installer for pyenv
- [direnv](https://direnv.net/) - Environment variable management tool that works well with pyenv

### Community Resources
- [Stack Overflow - pyenv tag](https://stackoverflow.com/questions/tagged/pyenv) - Community Q&A
- [Stack Overflow - venv tag](https://stackoverflow.com/questions/tagged/venv) - Community Q&A
- [r/Python subreddit](https://www.reddit.com/r/Python/) - Python community discussions
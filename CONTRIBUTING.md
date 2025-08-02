# Contributing to Halo

## Development Setup

1. Clone the repository
2. Install development dependencies:

   ```bash
   pip install -r requirements.txt
   pip install -e .[dev]
   ```

## Code Quality

This project uses several tools to maintain code quality:

- **Black**: Code formatting
- **isort**: Import sorting
- **flake8**: Linting
- **mypy**: Type checking
- **pylint**: Additional linting
- **pytest**: Testing with coverage

### Running Quality Checks Locally

```bash
# Format code
black .
isort .

# Lint code
flake8 .
mypy src/halo
pylint src/halo

# Run tests
pytest tests/ -v --cov=halo
```

## CI/CD Pipeline

The project uses GitHub Actions for continuous integration and deployment:

### Workflows

1. **CI/CD Pipeline** (`.github/workflows/ci.yml`):
   - Runs tests on Python 3.8-3.12 across Windows, macOS, and Linux
   - Performs security scans
   - Builds the package
   - Publishes to TestPyPI on main branch pushes
   - Publishes to PyPI on releases

2. **Code Quality** (`.github/workflows/code-quality.yml`):
   - Runs formatting and linting checks
   - Auto-formats code on develop branch

3. **Dependency Updates** (`.github/workflows/dependencies.yml`):
   - Weekly automated dependency updates
   - Security vulnerability checks

### Publishing to PyPI

#### Test PyPI (Automatic)

- Pushes to `main` branch automatically publish to TestPyPI
- Requires trusted publishing setup in TestPyPI

#### Production PyPI (Manual)

1. Create a GitHub release with a version tag
2. The release triggers automatic publishing to PyPI
3. Requires trusted publishing setup in PyPI

### Setting up Trusted Publishing

1. Go to PyPI/TestPyPI project settings
2. Configure "Trusted Publishing" with your GitHub repository
3. Set the workflow name to `ci.yml`
4. Set the environment name to `pypi` or `testpypi`

## Release Process

1. Update version in `src/halo/__init__.py`
2. Update `CHANGELOG.md`
3. Create a pull request to `main`
4. After merging, create a GitHub release with the version tag
5. The CI/CD pipeline will automatically publish to PyPI

## Branch Strategy

- `main`: Production-ready code
- `develop`: Development branch for new features
- Feature branches: `feature/feature-name`
- Bug fixes: `bugfix/bug-description`

## Testing

- Write tests for all new features and bug fixes
- Maintain test coverage above 80%
- Tests run automatically on all pull requests

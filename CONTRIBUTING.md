# Contributing to Citation Grabber

First off, thank you for considering contributing to Citation Grabber! It's people like you that make this tool better for everyone.

## Code of Conduct

Be respectful, constructive, and professional in all interactions.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues to avoid duplicates. When creating a bug report, include:

- **Clear title and description**
- **Steps to reproduce** the issue
- **Expected behavior** vs actual behavior
- **Python version** and operating system
- **Error messages** or logs (if any)

**Example:**

```markdown
**Title:** Citation fetch fails for DOI 10.xxxx/yyyy

**Description:**
When I try to fetch a citation using a specific DOI, the tool returns an error.

**Steps to Reproduce:**
1. Run `python3 citation.py "10.1234/example"`
2. See error message

**Expected:** Should return BibTeX citation
**Actual:** Returns "API Error: ..."

**Environment:**
- Python: 3.10.5
- OS: macOS 13.0
- citation-grabber: 1.1.0
```

### Suggesting Enhancements

Enhancement suggestions are welcome! Please provide:

- **Clear use case**: Why would this feature be useful?
- **Detailed description**: How should it work?
- **Examples**: Show what the usage would look like

### Pull Requests

1. **Fork** the repository
2. **Create a branch** from `main`:
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Make your changes**:
   - Follow the code style (use `black` for formatting)
   - Add tests for new features
   - Update documentation
4. **Test your changes**:
   ```bash
   pytest tests/
   ```
5. **Commit** with clear messages:
   ```bash
   git commit -m "Add support for arXiv citations"
   ```
6. **Push** to your fork:
   ```bash
   git push origin feature/amazing-feature
   ```
7. **Open a Pull Request**

## Development Setup

### Prerequisites

- Python 3.8 or higher
- pip

### Setup

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/citation-grabber.git
cd citation-grabber

# Create virtual environment (optional but recommended)
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install in development mode with dev dependencies
pip install -e ".[dev]"
```

### Running Tests

```bash
# Run all tests
pytest tests/

# Run with coverage
pytest tests/ --cov=citation --cov-report=html

# Run only unit tests (skip integration)
pytest tests/ -m "not integration"

# Run with verbose output
pytest tests/ -v
```

### Code Style

We use `black` for code formatting:

```bash
# Format code
black citation.py tests/

# Check formatting without changes
black --check citation.py tests/
```

We use `mypy` for type checking:

```bash
mypy citation.py
```

We use `flake8` for linting:

```bash
flake8 citation.py tests/
```

## Coding Guidelines

### Python Style

- Follow [PEP 8](https://pep8.org/)
- Use `black` with default settings
- Maximum line length: 100 characters
- Use type hints for all functions
- Write docstrings for all public functions

### Function Documentation

Use Google-style docstrings:

```python
def fetch_citation(doi: str, format: str = 'bibtex') -> Optional[str]:
    """
    Fetch citation by DOI.

    Args:
        doi: Digital Object Identifier
        format: Output format ('bibtex' or 'nbib')

    Returns:
        Citation string if found, None otherwise

    Raises:
        APIError: If the API request fails

    Examples:
        >>> fetch_citation("10.1234/example")
        '@article{...}'
    """
    pass
```

### Testing

- Write tests for all new features
- Maintain or improve code coverage
- Use descriptive test names
- Mock external API calls in unit tests
- Mark integration tests with `@pytest.mark.integration`

**Example:**

```python
def test_fetch_by_doi_successful():
    """Test that fetch_by_doi returns citation for valid DOI."""
    # Arrange
    doi = "10.1234/example"

    # Act
    result = fetch_by_doi(doi)

    # Assert
    assert result is not None
    assert doi in result
```

### Error Handling

- Use specific exception types
- Provide helpful error messages
- Log errors appropriately
- Don't catch exceptions silently

**Good:**
```python
try:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
except requests.exceptions.Timeout:
    logger.error(f"Timeout while fetching {url}")
    raise APIError(f"Request timed out")
except requests.exceptions.RequestException as e:
    logger.error(f"Request failed: {e}")
    raise APIError(f"Network error: {e}")
```

**Bad:**
```python
try:
    response = requests.get(url)
    return response.json()
except:
    pass
```

## Project Structure

```
citation-grabber/
├── citation.py              # Main module (keep monolithic for now)
├── tests/
│   ├── test_citation.py     # Unit tests
│   └── test_integration.py  # Integration tests
├── requirements.txt         # Runtime dependencies
├── pyproject.toml          # Project metadata and config
├── README.md               # User documentation
├── SKILL.md                # OpenClaw skill metadata
├── CONTRIBUTING.md         # This file
├── CHANGELOG.md            # Version history
└── LICENSE                 # MIT License
```

## Adding New Features

When adding new features:

1. **Discuss first**: Open an issue to discuss the feature
2. **Design**: Think about the API and user experience
3. **Implement**: Write the code with tests
4. **Document**: Update README.md and docstrings
5. **Test**: Ensure all tests pass
6. **Update**: Add entry to CHANGELOG.md

## Questions?

Feel free to open an issue with the `question` label or reach out to the maintainers.

## Recognition

Contributors will be recognized in the README and release notes.

---

Thank you for contributing to Citation Grabber! 🎉

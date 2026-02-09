# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-02-09

### Added
- Type hints throughout the codebase
- Comprehensive docstrings for all functions
- Structured exception handling with custom exception classes
- Detailed logging system with progress tracking
- Better error messages and user feedback
- `--quiet` flag for suppressing progress messages
- `--version` flag to show version information
- Batch processing progress indicators
- Unit tests with pytest
- Integration tests for real API calls
- Project configuration with pyproject.toml
- MIT License
- .gitignore for Python projects
- Comprehensive README with examples
- CONTRIBUTING guidelines
- This CHANGELOG

### Changed
- Improved error handling (no more silent failures)
- Better API timeout handling
- More informative output messages
- Enhanced command-line help text
- Updated SKILL.md with detailed examples
- Upgraded requirements.txt with version constraints

### Fixed
- Exception handling now provides specific error messages
- API timeouts are properly caught and reported
- Empty queries are now handled gracefully
- File I/O errors are properly caught

## [1.0.0] - 2026-01-XX

### Added
- Initial release
- Basic citation fetching from PubMed and CrossRef
- Support for BibTeX and NBIB formats
- Title, DOI, and PMID search
- Batch processing from text files
- Basic command-line interface

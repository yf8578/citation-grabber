# Citation Grabber 📚

> **Instantly fetch scientific paper citations in BibTeX or NBIB format.**

[![Python Version](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Citation Grabber** is a powerful command-line tool that searches for academic papers and retrieves high-quality citation metadata from multiple authoritative sources.

## ✨ Features

- **Multiple Input Methods**:
  - 📝 Search by paper title
  - 🔗 Direct DOI lookup
  - 🔢 Direct PubMed ID (PMID) lookup
  - 📄 Batch processing from text files

- **Dual Source Strategy**:
  - **PubMed (NCBI)**: Primary source for biomedical literature
  - **CrossRef**: Comprehensive fallback for all scientific disciplines

- **Flexible Output Formats**:
  - `BibTeX`: Standard format for LaTeX/Overleaf
  - `.nbib`: PubMed format for EndNote/Zotero import

- **Robust Error Handling**:
  - Detailed logging and progress tracking
  - Graceful fallback between data sources
  - Informative error messages

- **Developer-Friendly**:
  - Type hints throughout
  - Comprehensive test suite
  - Well-documented code
  - Modular design

## 🚀 Quick Start

### Installation

#### Option 1: Direct Usage (Recommended)

```bash
# Clone the repository
git clone https://github.com/yf8578/citation-grabber.git
cd citation-grabber

# Install dependencies
pip install -r requirements.txt

# Run the tool
python3 citation.py "Attention Is All You Need"
```

#### Option 2: Install as Package

```bash
pip install git+https://github.com/yf8578/citation-grabber.git

# Use as command
citation-grabber "Your Paper Title"
```

### Basic Usage

#### Single Paper by Title

```bash
python3 citation.py "Attention Is All You Need"
```

**Output:**
```bibtex
% Source: CrossRef (DOI: 10.5555/3295222.3295349)
@inproceedings{Vaswani_2017,
  title={Attention is all you need},
  author={Vaswani, Ashish and Shazeer, Noam and ...},
  year={2017}
}
```

#### By DOI

```bash
python3 citation.py "10.1038/nature14539"
```

#### By PubMed ID

```bash
python3 citation.py "12345678"
```

#### Get NBIB Format (for EndNote/Zotero)

```bash
python3 citation.py "COVID-19 vaccine effectiveness" --format nbib
```

### Batch Processing

Create a text file with paper titles (one per line):

**papers.txt:**
```text
Deep Residual Learning for Image Recognition
BERT: Pre-training of Deep Bidirectional Transformers
Attention Is All You Need
```

Process all papers at once:

```bash
python3 citation.py papers.txt --output references.bib
```

**Output:**
```
📂 Loaded 3 queries from file.

[1/3] Processing...
🔍 Processing: Deep Residual Learning for Image Recognition (Type: title)
✓ Found via DOI: 10.1109/CVPR.2016.90

[2/3] Processing...
🔍 Processing: BERT: Pre-training of Deep Bidirectional Transformers (Type: title)
✓ Found via DOI: 10.18653/v1/N19-1423

[3/3] Processing...
🔍 Processing: Attention Is All You Need (Type: title)
✓ Found via DOI: 10.5555/3295222.3295349

✅ Saved 3 citation(s) to references.bib
📊 Summary: 3/3 successful
```

## 📖 Command-Line Options

```
usage: citation.py [-h] [--format {bibtex,nbib}] [--output OUTPUT] [--quiet] [--version] input

Fetch citations (BibTeX/NBIB) from Title, DOI, or PMID.

positional arguments:
  input                 Title, DOI, PMID, or path to .txt file with multiple queries

options:
  -h, --help            show this help message and exit
  --format {bibtex,nbib}
                        Output format (default: bibtex)
  --output OUTPUT, -o OUTPUT
                        Output file path (default: print to stdout)
  --quiet, -q           Suppress progress messages
  --version             show program's version number and exit
```

## 🔧 Advanced Usage

### Quiet Mode

Suppress progress messages (useful for scripts):

```bash
python3 citation.py "Paper Title" --quiet > output.bib
```

### Mix of Input Types

You can include titles, DOIs, and PMIDs in the same batch file:

**mixed_queries.txt:**
```text
Attention Is All You Need
10.1038/nature14539
12345678
Deep Learning Review
```

```bash
python3 citation.py mixed_queries.txt --output citations.bib
```

## 🧪 Testing

The project includes comprehensive unit tests and integration tests.

### Run Unit Tests

```bash
# Install test dependencies
pip install pytest pytest-cov pytest-mock

# Run tests
pytest tests/

# Run with coverage report
pytest tests/ --cov=citation --cov-report=html
```

### Run Integration Tests

Integration tests make real API calls:

```bash
pytest tests/ -m integration
```

### Skip Integration Tests

```bash
pytest tests/ -m "not integration"
```

## 📁 Project Structure

```
citation-grabber/
├── citation.py           # Main module
├── requirements.txt      # Dependencies
├── pyproject.toml       # Project metadata
├── LICENSE              # MIT License
├── README.md            # This file
├── SKILL.md             # OpenClaw skill metadata
├── .gitignore           # Git ignore rules
├── pytest.ini           # Pytest configuration
└── tests/               # Test suite
    ├── __init__.py
    ├── test_citation.py      # Unit tests
    └── test_integration.py   # Integration tests
```

## 🎯 How It Works

1. **Input Detection**: Automatically detects whether input is a DOI, PMID, or title
2. **Smart Search Strategy**:
   - For DOIs: Direct lookup via doi.org
   - For PMIDs: Direct fetch from PubMed
   - For titles:
     - If NBIB format requested: Try PubMed first
     - Otherwise: Try CrossRef first (better BibTeX quality)
     - Fallback to alternative source if primary fails
3. **Result Formatting**: Returns properly formatted citations with source attribution

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Report Bugs**: Open an issue describing the problem
2. **Suggest Features**: Share your ideas in the issues
3. **Submit PRs**:
   - Fork the repository
   - Create a feature branch
   - Add tests for new functionality
   - Ensure all tests pass
   - Submit a pull request

### Development Setup

```bash
# Clone and install dev dependencies
git clone https://github.com/yf8578/citation-grabber.git
cd citation-grabber
pip install -e ".[dev]"

# Run tests
pytest tests/

# Format code
black citation.py tests/

# Type checking
mypy citation.py
```

## 🐛 Known Limitations

- CrossRef and PubMed availability depends on their API uptime
- Title searches may return incorrect papers for very generic titles
- Some older papers may not be available in digital databases
- Rate limiting may apply for large batch operations

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [CrossRef](https://www.crossref.org/) for their comprehensive DOI database
- [NCBI PubMed](https://pubmed.ncbi.nlm.nih.gov/) for biomedical literature access
- All contributors to this project

## 📧 Contact

- **Issues**: [GitHub Issues](https://github.com/yf8578/citation-grabber/issues)
- **Author**: yf8578

## 🔗 Related Projects

- [crossref-commons](https://github.com/CrossRef/crossref-commons-py) - Python library for CrossRef API
- [biopython](https://biopython.org/) - Tools for biological computation including PubMed access
- [doi2bib](https://www.doi2bib.org/) - Web-based DOI to BibTeX converter

---

⭐ If you find this tool useful, please consider giving it a star on GitHub!

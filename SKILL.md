---
name: citation-grabber
description: Search for scientific papers and fetch citations in BibTeX or NBIB format from PubMed and CrossRef
version: 1.1.0
usage: citation-grabber <title_or_doi_or_pmid_or_file> [--format bibtex|nbib] [--output <file>] [--quiet]
metadata:
  openclaw:
    emoji: "📚"
    os: ["darwin", "linux", "win32"]
    requires:
      bins: ["python3"]
      python: ">=3.8"
    install:
      - id: pip-deps
        kind: pip
        packages: ["requests>=2.25.0"]
        label: "Install Python dependencies"
---

# Citation Grabber

Instantly fetch scientific paper citations from the command line.

## Features

- 🔍 Search by **title**, **DOI**, or **PubMed ID**
- 📚 Supports **BibTeX** and **NBIB** output formats
- 🔄 Dual source: **PubMed** + **CrossRef**
- 📦 Batch processing from text files
- ✨ Smart fallback between data sources

## Installation

The skill automatically ensures dependencies are installed. Manual installation:

```bash
pip3 install requests>=2.25.0
```

## Usage

### Single Paper

**By Title:**
```bash
python3 citation.py "Attention Is All You Need"
```

**By DOI:**
```bash
python3 citation.py "10.1038/nature14539"
```

**By PubMed ID:**
```bash
python3 citation.py "12345678"
```

### Output Formats

**BibTeX (Default):**
```bash
python3 citation.py "Deep Learning" --format bibtex
```

**NBIB (PubMed Format for EndNote/Zotero):**
```bash
python3 citation.py "COVID-19 vaccine" --format nbib
```

### Batch Processing

Create a file `papers.txt` with paper titles/DOIs/PMIDs (one per line):

```text
Attention Is All You Need
10.1038/nature14539
Deep Residual Learning for Image Recognition
```

Process all at once:

```bash
python3 citation.py papers.txt --output references.bib
```

### Save to File

```bash
python3 citation.py "Paper Title" --output my_citations.bib
```

### Quiet Mode

Suppress progress messages (useful for scripting):

```bash
python3 citation.py "Paper Title" --quiet
```

## Command-Line Options

| Option | Short | Description | Default |
|--------|-------|-------------|---------|
| `--format` | | Output format: `bibtex` or `nbib` | `bibtex` |
| `--output` | `-o` | Save to file instead of stdout | stdout |
| `--quiet` | `-q` | Suppress progress messages | `false` |
| `--version` | | Show version and exit | - |
| `--help` | `-h` | Show help message | - |

## Examples

**Get BibTeX for a Classic Paper:**
```bash
python3 citation.py "The structure of DNA"
```

**Get NBIB for a Medical Paper:**
```bash
python3 citation.py "COVID-19 vaccine effectiveness" --format nbib
```

**Process a List of Papers:**
```bash
# Create papers.txt
echo "Attention Is All You Need" > papers.txt
echo "BERT: Pre-training of Deep Bidirectional Transformers" >> papers.txt
echo "Deep Residual Learning for Image Recognition" >> papers.txt

# Fetch all citations
python3 citation.py papers.txt --output all_refs.bib
```

**Silent Mode for Scripts:**
```bash
python3 citation.py "10.1038/nature14539" --quiet > paper.bib 2>/dev/null
```

## How It Works

1. **Auto-Detection**: Identifies input type (title, DOI, or PMID)
2. **Smart Search**:
   - Direct DOI → Fetch from doi.org
   - Direct PMID → Fetch from PubMed
   - Title search → Try CrossRef first, fallback to PubMed
3. **Robust Fallback**: If one source fails, automatically tries the other

## Tips

- For **biomedical papers**, use `--format nbib` to get PubMed-native format
- For **LaTeX/Overleaf**, use default `--format bibtex`
- Use **DOI or PMID** when available for faster and more accurate results
- Create a **papers.txt** file to manage your bibliography systematically

## Troubleshooting

**No citation found:**
- Verify the paper title is correct (check for typos)
- Try using DOI or PMID instead of title
- Some older papers may not be in digital databases

**Timeout errors:**
- Check your internet connection
- APIs may be temporarily unavailable
- Try again after a few moments

**Wrong paper returned:**
- Use more specific titles
- Prefer DOI or PMID for exact matching
- Verify the returned citation before use

## Requirements

- Python 3.8 or higher
- `requests` library (auto-installed by skill)
- Internet connection

## Version History

- **1.1.0**: Complete rewrite with type hints, better error handling, comprehensive tests
- **1.0.0**: Initial release

## Links

- **Repository**: https://github.com/yf8578/citation-grabber
- **Issues**: https://github.com/yf8578/citation-grabber/issues
- **License**: MIT

# pdf-text-extract

Extract text from PDFs - handles both digital text and scanned pages via OCR.

## The Problem

Academic papers, legal documents, and old scans often come as PDFs. Some have selectable text (digital), others are just images of text (scanned). Most tools handle one or the other, not both.

This tool automatically detects which type you have and uses the right extraction method.

## How It Works

1. **Auto-detect** - Samples the first couple pages to check for extractable text
2. **Text-based PDFs** - Uses pdftotext (fast, preserves layout)
3. **Scanned PDFs** - Uses Tesseract OCR at configurable DPI
4. **Cleans output** - Strips common academic headers/footers (page numbers, copyright lines, DOIs, etc.)

## Installation

```bash
# System dependencies (Ubuntu/Debian)
sudo apt install poppler-utils tesseract-ocr

# Python dependencies
pip install pdfplumber pdf2image pytesseract
```

## Usage

```bash
# Basic usage (auto-detects, outputs to input.txt)
python3 extract.py document.pdf

# Specify output file
python3 extract.py document.pdf output.txt

# Force OCR even for text PDFs
python3 extract.py document.pdf --force-ocr

# Force pdftotext even if PDF looks scanned
python3 extract.py document.pdf --force-text

# Adjust OCR quality (higher DPI = better quality, slower)
python3 extract.py document.pdf --dpi 300

# Add custom header patterns to strip (regex)
python3 extract.py document.pdf --headers "AUTHOR NAME" "JOURNAL TITLE"

# Skip header/footer cleaning
python3 extract.py document.pdf --no-clean
```

## Default Headers Stripped

- Standalone page numbers
- Copyright lines
- "Access provided by" lines
- DOI lines
- JSTOR/MUSE URLs
- "Published by X Press" lines

## Why This Exists

Built for extracting text from academic papers - the kind that are sometimes scanned from old journals, sometimes digital but with weird encodings, sometimes a mix of both.

Original use case: Converting pre-law course PDFs to text for ElevenReader (text-to-speech).

## License

MIT

## Author

[Eli](https://github.com/someone-inside) - January 2026

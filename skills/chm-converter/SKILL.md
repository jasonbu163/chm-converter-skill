---
name: "chm-converter"
description: "Converts CHM files to Markdown format, optimized for Revit API documentation. Invoke when user needs to convert CHM help files to readable markdown format."
---

# CHM to Markdown Converter

This skill converts Compiled HTML Help (CHM) files to well-formatted Markdown files, specifically optimized for Revit API documentation.

## Features

- **Multi-version Support**: Processes multiple Revit API documentation versions (2022-2026)
- **Organized Output**: Creates structured folder hierarchy with core/ and data/ directories
- **AI Integration Ready**: Generates index files for search functionality and AI integration
- **Code Snippet Handling**: Preserves and formats code snippets with language-specific syntax highlighting
- **Link Preservation**: Updates internal links to maintain document references
- **Asynchronous Processing**: Batch processes multiple files with progress reporting
- **Performance Optimized**: Configurable worker threads and batch sizes

## Usage

### Quick Start

1. **Place CHM files** in the `resources/` directory
2. **Run the converter**:
```bash
python chm_to_markdown.py
```
3. **Find output** in the `output/` directory with organized version folders

### Basic Usage
```bash
# Interactive mode - choose specific CHM file or process all
python chm_to_markdown.py
```

### Command Line Options
```bash
# Process single CHM file
python chm_to_markdown.py --single resources/2024.chm

# Process all CHM files in resources folder
python chm_to_markdown.py --all

# Keep HTML files after conversion (for debugging)
python chm_to_markdown.py --all --keep-html

# Performance tuning (useful for large batches)
python chm_to_markdown.py --all --workers 4 --batch-size 25 --semaphore 10
```

### Common Workflows

```bash
# Single file conversion with progress
python chm_to_markdown.py --single resources/Revit2024.chm

# Batch process all versions
python chm_to_markdown.py --all

# Full conversion with HTML debugging
python chm_to_markdown.py --all --keep-html

# High-performance processing
python chm_to_markdown.py --all --workers 8 --batch-size 50
```

## Output Structure

```
output/
├── 2022/
│   ├── core/           # Index files for AI and search
│   │   ├── file_index.json
│   │   ├── id_lookup.json
│   │   └── index.md
│   └── data/           # Markdown documentation files
│       ├── APIReference.md
│       ├── ClassLibrary.md
│       └── ...
└── 2024/
    ├── core/
    │   ├── file_index.json    # Maps file IDs to metadata
    │   ├── id_lookup.json     # Keyword lookup dictionary
    │   └── index.md           # Navigation guide
    └── data/
        └── ...
```

### Output File Examples

**file_index.json:**
```json
{
  "APIReference.md": {"id": "1", "title": "API Reference", "version": "2024"},
  "ClassLibrary.md": {"id": "2", "title": "Class Library", "version": "2024"}
}
```

**Sample Markdown Output:**
```markdown
# API Reference (2024)

## Namespace: Autodesk.Revit.DB

### Class: Element
Base class for all elements in Revit document.

**Properties:**
- `Id`: Element identifier
- `Name`: Element display name

**Code Example:**
\`\`\`csharp
Element element = doc.GetElement(eid);
string name = element.Name;
\`\`\`
```

## Requirements

- Python 3.7+
- 7-Zip installed (Windows: `C:\Program Files\7-Zip\7z.exe`, Linux/macOS: `7z` or `7zz`)
- Python packages: `beautifulsoup4`, `html2text`, `aiofiles`
- CHM 文件存放在 `resources/` 目录中

## Environment Setup

### Check Python Version
```bash
python --version  # Should be 3.7 or higher
```

### Check 7-Zip Installation

**macOS:**
```bash
which 7z        # or
which 7zz       # Check if 7-Zip is installed
brew install p7zip  # Install if needed
```

**Windows:**
```bash
dir "C:\Program Files\7-Zip\7z.exe"
```

**Linux:**
```bash
which 7z
sudo apt-get install p7zip-full  # Install if needed
```

## Installation

```bash
# Clone or navigate to the project directory
cd chm-converter

# Install dependencies
pip install -r requirements.txt
# or manually install
pip install beautifulsoup4 html2text aiofiles

# Verify installation
python -c "import bs4, html2text, aiofiles; print('All dependencies installed!')"
```

## Customization

### Content Filtering
Modify these lists in the script to customize HTML element removal:
- `tags_to_remove`: HTML tags to remove
- `classes_to_remove`: CSS classes to remove
- `ids_to_remove`: Element IDs to remove

### Code Language Mapping
Update `id_to_lang` dictionary for language-specific code formatting:
```python
id_to_lang = {
    "IDAB_code_Div1": "csharp",
    "IDAB_code_Div2": "vb",
    "IDAB_code_Div3": "cpp",
    "IDAB_code_Div4": "fsharp",
}
```

## AI Integration Features

- **file_index.json**: Maps file IDs to titles and versions
- **id_lookup.json**: Provides keyword lookup dictionary
- **index.md**: User-friendly navigation structure
- Version information embedded in markdown headings
- Maintained internal document references

## Troubleshooting

### Issue: "7-Zip not found" error

**Solution:**
```bash
# macOS
brew install p7zip

# Linux
sudo apt-get install p7zip-full

# Windows - Verify installation path
# C:\Program Files\7-Zip\7z.exe should exist
```

### Issue: "No CHM files found"

**Check:**
1. Create `resources/` directory if it doesn't exist: `mkdir resources`
2. Place CHM files in `resources/` folder
3. Verify files: `ls -la resources/`

### Issue: "ModuleNotFoundError: No module named 'bs4'"

**Solution:**
```bash
pip install --upgrade beautifulsoup4 html2text aiofiles
python -c "import bs4; print(bs4.__version__)"
```

### Issue: Slow processing or memory issues

**Solutions:**
- Reduce `--workers` value: `--workers 2`
- Reduce `--batch-size`: `--batch-size 10`
- Process files individually: `--single resources/one_file.chm`

### Issue: Corrupted output files

**Solution:**
```bash
# Clean up and retry
rm -rf output/
python chm_to_markdown.py --all --keep-html  # Keep HTML for debugging
```
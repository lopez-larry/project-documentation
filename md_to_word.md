# Markdown to Word Conversion Script

## Overview

This script scans a directory of Markdown (`.md`) files and generates corresponding Microsoft Word (`.docx`) documents. It is designed to automate template generation and standardize document output.

---

## Directory Structure

```

.
├── Templates/        # Input directory (contains .md files)
├── Word-Template/    # Output directory (generated .docx files)
├── md_to_word.py     # Script

````

---

## Purpose

The script performs the following:

- Reads all `.md` files from `./Templates`
- Converts each file into a `.docx` document
- Writes the output to `./Word-Template`
- Preserves basic Markdown structure (headings, lists, paragraphs, code blocks)

---

## Dependencies

The script uses:

- `python-docx` → for Word document generation

Install dependency:

```bash
pip install python-docx
````

---

## Execution

Run the script from the root directory:

```bash
python3 md_to_word.py
```

---

## High-Level Workflow

### Step 1: Validate Directories

* Confirms `./Templates` exists
* Creates `./Word-Template` if it does not exist

---

### Step 2: Locate Markdown Files

* Scans `./Templates` for all `.md` files
* Stores file list for processing

---

### Step 3: Process Each File

For each `.md` file:

1. Open file
2. Read line-by-line
3. Interpret Markdown syntax
4. Convert to Word document format

---

### Step 4: Convert Markdown Elements

The script translates Markdown into Word formatting:

#### Headings

```
# Heading 1 → Word Heading Level 1
## Heading 2 → Word Heading Level 2
...
```

#### Bullet Lists

```
- Item
* Item
+ Item
```

→ Converted to Word bullet list style

---

#### Numbered Lists

```
1. Item
2. Item
```

→ Converted to Word numbered list style

---

#### Paragraphs

* Plain text lines become standard paragraphs
* Blank lines create spacing

---

#### Code Blocks

```
```

code here

```
```

→ Converted to:

* Monospace font (`Courier New`)
* Preserved formatting

---

### Step 5: Save Output

* Output file name matches input file name
* Example:

```
Templates/example.md → Word-Template/example.docx
```

---

## Supported Features

| Feature        | Supported |
| -------------- | --------- |
| Headings       | Yes       |
| Bullet Lists   | Yes       |
| Numbered Lists | Yes       |
| Paragraphs     | Yes       |
| Code Blocks    | Yes       |
| Blank Lines    | Yes       |

---

## Limitations

This is a lightweight converter and does **not** support:

* Tables
* Images
* Links (formatted)
* Bold / Italics
* Nested lists (advanced formatting)
* Markdown extensions (GitHub-style)

---

## Error Handling

* If `Templates/` does not exist → script stops with error
* If no `.md` files found → prints message and exits
* If conversion fails for a file → logs error and continues

---

## Example Output

Input:

```md
# Project Plan

## Tasks

- Define scope
- Assign roles

1. Start project
2. Monitor progress
```

Output:

* Word document with:

  * Proper heading hierarchy
  * Bullet list
  * Numbered list

---

## Use Cases

* Document template generation
* Project documentation conversion
* Markdown → Word reporting
* Standardized output for stakeholders

---

## Summary

This script provides a simple pipeline:

```
Markdown Files → Parsing → Word Document Generation → Output Directory
```

It is best suited for:

* Structured documents
* Lightweight formatting
* Automated template workflows

---

## Future Enhancements (Optional)

* Add support for:

  * Bold / italic formatting
  * Tables
  * Images
  * Hyperlinks
* Add CLI arguments for custom directories
* Add logging and reporting summary
* Integrate with CI/CD pipelines



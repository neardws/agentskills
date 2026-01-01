---
name: pdf-processing
description: Extract text and tables from PDF files, create PDFs, fill forms, and merge/split documents. Use when working with PDF documents, extracting content, or generating PDF reports.
---

# PDF Processing Skill

This skill enables reading, creating, and manipulating PDF documents.

## Dependencies

```bash
pip install PyPDF2 pdfplumber reportlab
```

For OCR on scanned PDFs:
```bash
pip install pdf2image pytesseract
# Also requires: brew install tesseract poppler (macOS)
```

## Extracting Text

### Using PyPDF2 (basic)
```python
from PyPDF2 import PdfReader

reader = PdfReader('document.pdf')
for page in reader.pages:
    text = page.extract_text()
    print(text)
```

### Using pdfplumber (better formatting)
```python
import pdfplumber

with pdfplumber.open('document.pdf') as pdf:
    for page in pdf.pages:
        text = page.extract_text()
        print(text)
```

## Extracting Tables

```python
import pdfplumber

with pdfplumber.open('document.pdf') as pdf:
    page = pdf.pages[0]
    tables = page.extract_tables()
    for table in tables:
        for row in table:
            print(row)
```

## Creating PDFs

```python
from reportlab.lib.pagesizes import letter, A4
from reportlab.pdfgen import canvas
from reportlab.lib.units import inch

c = canvas.Canvas('output.pdf', pagesize=letter)
width, height = letter

# Add text
c.setFont('Helvetica-Bold', 16)
c.drawString(1*inch, height - 1*inch, 'Document Title')

c.setFont('Helvetica', 12)
c.drawString(1*inch, height - 1.5*inch, 'This is paragraph text.')

# Add image
c.drawImage('image.png', 1*inch, height - 4*inch, width=3*inch, height=2*inch)

# New page
c.showPage()

c.save()
```

## Merging PDFs

```python
from PyPDF2 import PdfMerger

merger = PdfMerger()
merger.append('file1.pdf')
merger.append('file2.pdf')
merger.append('file3.pdf', pages=(0, 5))  # Only pages 0-4
merger.write('merged.pdf')
merger.close()
```

## Splitting PDFs

```python
from PyPDF2 import PdfReader, PdfWriter

reader = PdfReader('document.pdf')

# Extract single page
writer = PdfWriter()
writer.add_page(reader.pages[0])
with open('page1.pdf', 'wb') as f:
    writer.write(f)

# Split into individual pages
for i, page in enumerate(reader.pages):
    writer = PdfWriter()
    writer.add_page(page)
    with open(f'page_{i+1}.pdf', 'wb') as f:
        writer.write(f)
```

## PDF Metadata

```python
from PyPDF2 import PdfReader, PdfWriter

reader = PdfReader('document.pdf')

# Read metadata
meta = reader.metadata
print(f"Title: {meta.title}")
print(f"Author: {meta.author}")
print(f"Pages: {len(reader.pages)}")

# Write metadata
writer = PdfWriter()
for page in reader.pages:
    writer.add_page(page)
writer.add_metadata({
    '/Title': 'New Title',
    '/Author': 'Author Name'
})
with open('output.pdf', 'wb') as f:
    writer.write(f)
```

## OCR for Scanned PDFs

```python
from pdf2image import convert_from_path
import pytesseract

images = convert_from_path('scanned.pdf')
for i, image in enumerate(images):
    text = pytesseract.image_to_string(image, lang='eng')
    print(f"Page {i+1}:\n{text}")
```

## Best Practices

1. Use `pdfplumber` for better text extraction with layout preservation.
2. For large PDFs, process pages one at a time to manage memory.
3. Always close file handles and use context managers.
4. Check if PDF is encrypted before processing: `reader.is_encrypted`.
5. For form filling, consider `pdfrw` or `PyPDF2` with AcroForm support.

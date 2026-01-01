---
name: docx
description: Create, read, and edit Microsoft Word (.docx) documents. Use when working with Word files, generating reports, or formatting text documents.
---

# Word Document Processing Skill

This skill enables creating, reading, and modifying Microsoft Word documents.

## Dependencies

Requires `python-docx` library:
```bash
pip install python-docx
```

## Creating a Document

```python
from docx import Document
from docx.shared import Inches, Pt
from docx.enum.text import WD_ALIGN_PARAGRAPH

doc = Document()

# Add title
title = doc.add_heading('Document Title', 0)
title.alignment = WD_ALIGN_PARAGRAPH.CENTER

# Add paragraph
doc.add_paragraph('This is a paragraph with some text.')

# Add formatted text
p = doc.add_paragraph()
p.add_run('Bold text').bold = True
p.add_run(' and ')
p.add_run('italic text').italic = True

# Add bullet list
doc.add_paragraph('Item 1', style='List Bullet')
doc.add_paragraph('Item 2', style='List Bullet')

# Add table
table = doc.add_table(rows=2, cols=3)
table.style = 'Table Grid'
for i, cell in enumerate(table.rows[0].cells):
    cell.text = f'Header {i+1}'

# Add image
doc.add_picture('image.png', width=Inches(4))

doc.save('output.docx')
```

## Reading a Document

```python
from docx import Document

doc = Document('input.docx')

# Read all paragraphs
for para in doc.paragraphs:
    print(para.text)

# Read tables
for table in doc.tables:
    for row in table.rows:
        for cell in row.cells:
            print(cell.text)
```

## Common Operations

- **Styles**: `'Heading 1'`, `'Heading 2'`, `'Normal'`, `'List Bullet'`, `'List Number'`
- **Font size**: `run.font.size = Pt(12)`
- **Font color**: `run.font.color.rgb = RGBColor(0, 0, 255)`
- **Page break**: `doc.add_page_break()`
- **Section**: `doc.add_section()`

## Best Practices

1. Use consistent heading levels for document structure.
2. Apply styles instead of direct formatting for maintainability.
3. Always save with `.docx` extension.
4. Handle exceptions when opening files that may not exist.

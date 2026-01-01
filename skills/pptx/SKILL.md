---
name: pptx
description: Create, read, and edit Microsoft PowerPoint (.pptx) presentations. Use when building slideshows, generating presentation reports, or modifying slide content.
---

# PowerPoint Presentation Processing Skill

This skill enables creating, reading, and modifying PowerPoint presentations.

## Dependencies

Requires `python-pptx` library:
```bash
pip install python-pptx
```

## Creating a Presentation

```python
from pptx import Presentation
from pptx.util import Inches, Pt
from pptx.enum.text import PP_ALIGN
from pptx.dml.color import RGBColor

prs = Presentation()

# Title slide
slide_layout = prs.slide_layouts[0]  # Title Slide
slide = prs.slides.add_slide(slide_layout)
title = slide.shapes.title
subtitle = slide.placeholders[1]
title.text = "Presentation Title"
subtitle.text = "Subtitle goes here"

# Content slide with bullets
slide_layout = prs.slide_layouts[1]  # Title and Content
slide = prs.slides.add_slide(slide_layout)
title = slide.shapes.title
title.text = "Agenda"
body = slide.placeholders[1]
tf = body.text_frame
tf.text = "First bullet point"
p = tf.add_paragraph()
p.text = "Second bullet point"
p.level = 0
p = tf.add_paragraph()
p.text = "Sub-bullet"
p.level = 1

prs.save('output.pptx')
```

## Adding Images and Shapes

```python
# Blank slide
slide_layout = prs.slide_layouts[6]  # Blank
slide = prs.slides.add_slide(slide_layout)

# Add image
slide.shapes.add_picture('image.png', Inches(1), Inches(1), width=Inches(4))

# Add text box
txBox = slide.shapes.add_textbox(Inches(1), Inches(5), Inches(8), Inches(1))
tf = txBox.text_frame
tf.text = "Custom text box content"

# Add shape
from pptx.enum.shapes import MSO_SHAPE
shape = slide.shapes.add_shape(MSO_SHAPE.RECTANGLE, Inches(5), Inches(2), Inches(2), Inches(1))
shape.text = "Rectangle"
```

## Adding Tables

```python
slide_layout = prs.slide_layouts[5]  # Title Only
slide = prs.slides.add_slide(slide_layout)

rows, cols = 3, 4
table = slide.shapes.add_table(rows, cols, Inches(1), Inches(2), Inches(8), Inches(2)).table

# Set header row
for i, header in enumerate(['Col A', 'Col B', 'Col C', 'Col D']):
    table.cell(0, i).text = header

# Fill data
for row in range(1, rows):
    for col in range(cols):
        table.cell(row, col).text = f'R{row}C{col}'
```

## Reading a Presentation

```python
prs = Presentation('input.pptx')

for slide in prs.slides:
    for shape in slide.shapes:
        if shape.has_text_frame:
            for paragraph in shape.text_frame.paragraphs:
                print(paragraph.text)
```

## Slide Layouts Reference

| Index | Layout Name |
|-------|-------------|
| 0 | Title Slide |
| 1 | Title and Content |
| 2 | Section Header |
| 3 | Two Content |
| 4 | Comparison |
| 5 | Title Only |
| 6 | Blank |

## Best Practices

1. Use consistent slide layouts for professional look.
2. Keep text concise - slides are visual aids.
3. Use high-resolution images (300 DPI for printing).
4. Maintain consistent font sizes across slides.

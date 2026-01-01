---
name: xlsx
description: Create, read, and edit Microsoft Excel (.xlsx) spreadsheets. Use when working with tabular data, generating reports, or performing data analysis in Excel format.
---

# Excel Spreadsheet Processing Skill

This skill enables creating, reading, and modifying Excel spreadsheets.

## Dependencies

Requires `openpyxl` library:
```bash
pip install openpyxl
```

For reading older `.xls` files, also install:
```bash
pip install xlrd
```

## Creating a Spreadsheet

```python
from openpyxl import Workbook
from openpyxl.styles import Font, Alignment, Border, Side, PatternFill
from openpyxl.utils import get_column_letter

wb = Workbook()
ws = wb.active
ws.title = "Sheet1"

# Write data
ws['A1'] = 'Name'
ws['B1'] = 'Value'
ws.append(['Item 1', 100])
ws.append(['Item 2', 200])

# Style header row
header_font = Font(bold=True, size=12)
for cell in ws[1]:
    cell.font = header_font
    cell.alignment = Alignment(horizontal='center')

# Add formula
ws['B4'] = '=SUM(B2:B3)'

# Adjust column width
ws.column_dimensions['A'].width = 15

wb.save('output.xlsx')
```

## Reading a Spreadsheet

```python
from openpyxl import load_workbook

wb = load_workbook('input.xlsx')
ws = wb.active

# Read all rows
for row in ws.iter_rows(values_only=True):
    print(row)

# Read specific cell
value = ws['A1'].value

# Read range
for row in ws['A1:C10']:
    for cell in row:
        print(cell.value)
```

## Working with Multiple Sheets

```python
# Create new sheet
ws2 = wb.create_sheet('Data')

# Access sheet by name
ws = wb['Sheet1']

# List all sheets
print(wb.sheetnames)

# Copy sheet
wb.copy_worksheet(ws)
```

## Common Formatting

```python
from openpyxl.styles import PatternFill, Border, Side

# Background color
yellow_fill = PatternFill(start_color='FFFF00', fill_type='solid')
ws['A1'].fill = yellow_fill

# Borders
thin_border = Border(
    left=Side(style='thin'),
    right=Side(style='thin'),
    top=Side(style='thin'),
    bottom=Side(style='thin')
)
ws['A1'].border = thin_border

# Number format
ws['B2'].number_format = '#,##0.00'
ws['C2'].number_format = '0%'
```

## Best Practices

1. Use `iter_rows()` for memory-efficient reading of large files.
2. Apply number formats for currency, percentages, and dates.
3. Use named ranges for complex formulas.
4. Close workbooks after use to free resources.

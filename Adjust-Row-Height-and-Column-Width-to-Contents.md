![AdjustToContents.jpg](images/Adjust-Row-Height-and-Column-Width-to-Contents_AdjustToContents.jpg "AdjustToContents.jpg")  

```c#
var wb = new XLWorkbook();
var ws = wb.Worksheets.Add("Adjust To Contents");

// Set some values with different font sizes
ws.Cell(1, 1).Value = "Tall Row";
ws.Cell(1, 1).Style.Font.FontSize = 30;
ws.Cell(2, 1).Value = "Very Wide Column";
ws.Cell(2, 1).Style.Font.FontSize = 20;

// Adjust column width
ws.Column(1).AdjustToContents();

// Adjust row heights
ws.Rows(1, 2).AdjustToContents();

// You can also adjust all rows/columns in one shot
// ws.Rows().AdjustToContents();
// ws.Columns().AdjustToContents();

// We'll now select which cells should be used for calculating the
// column widths (same method applies for row heights)

// Set the values
ws.Cell(4, 2).Value = "Width ignored because calling column.AdjustToContents(5, 7)";
ws.Cell(5, 2).Value = "Short text";
ws.Cell(6, 2).Value = "Width ignored because it's part of a merge";
ws.Range(6, 2, 6, 4).Merge();
ws.Cell(7, 2).Value = "Width should adjust to this cell";
ws.Cell(8, 2).Value = "Width ignored because calling column.AdjustToContents(5, 7)";

// Adjust column widths only taking into account rows 5-7
// (merged cells will be ignored)
ws.Column(2).AdjustToContents(5, 7);

// You can also specify the row to start calculating the widths:
// e.g. ws.Column(3).AdjustToContents(9);

wb.SaveAs("AdjustToContents.xlsx");
```

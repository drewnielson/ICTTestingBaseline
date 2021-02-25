# 12. Tables

Accessibility Requirements
--------------------------
-   [WCAG SC 1.3.1 Info and Relationships](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html): Information, structure, and relationships conveyed through presentation can be programmatically determined or are available in text.

Test Method Rationale
---------------------
For assistive technology (AT) users, data tables must explicitly associate table data with table row and column headers via programmatic markup. Table markup also facilitates navigation for AT users by providing programmatic landmarks via column and row headers.

When `<table>` elements are used for layout purposes, data table structure elements are not permitted, such as `<th>`, `<caption>`, or `<summary>` (HTML4).

Limitations, Assumptions, Exceptions
------------------------------------
-   Data tables are those tables where information in a cell requires a row or column header to adequately describe the cell's contents. If a table is used for placement of components on the page for visual aesthetics, then it is considered a layout table.
-   Some content may visually appear to require a data table structure, but, linearizing the content and/or viewing the code reveals that the content is understandable without the table. This technique may be used for responsive design. These elements use CSS and/or other styling methods to present content in columns or rows. The information conveyed does not rely on programmatic relationships between column or row headers to be understood. This content is not a data table and should not use the element, ARIA role="table", and associated programmatic table attributes. It should be tested using other baseline tests, such as [13.Structure.md](https://github.com/Section508Coordinators/ICTTestingBaseline/blob/master/docs/13Headings.md) and/or possibly [10. Forms (associated instructions)](https://github.com/Section508Coordinators/ICTTestingBaseline/blob/master/docs/10Forms.md).
-   Rows of data that are related must have a row header so assistive technology users can understand the relationship of the row's data cells. Not every table requires a row header. For example, a calendar month is a data table, typically with the days of the week as column headers. The dates in a row are not related so typically, there is no row header present. However, if there was a cell in each row to indicate the week of the year, this cell would serve as a row header for the dates within that row.

12.1 Test Procedure for Data Tables
------------------------------------------------
**Baseline Test ID:** 12.1-DataTable
### Identify Content
All content/data visually presented in a table with column and/or row headers where the content is not in a meaningful sequence when linearized.

Note: Linearization of table content is the presentation of a table’s two-dimensional content in one-dimensional order of the content in the source, beginning with the first cell in the first row and ending with the last cell in the last row, from left to right, top to bottom.

### Test Instructions

1.  Table: Check that each data table has programmatic markup to identify it as a table using one of the following techniques [SC 1.3.1]:
    -   HTML `<table>`
    -   ARIA `role="table"`
    -   ARIA `role="grid"`
1.  Check that the data `<table>` element DOES NOT have `role="presentation"` or `role="none"`. [SC 1.3.1]
2.  Table data cell: Check that each data cell uses only one of the following methods to identify it as a data cell within a table row depending on the technique identified in the first step [SC 1.3.1]:
    -   For HTML `<table>`: `<td>` for the cell, which must be within a `<tr>` row.
    -   For ARIA `role="table"`: ARIA `role="cell"`, which must be within an ARIA `role="row"`.
    -   For ARIA `role="grid"`: ARIA `role="gridcell"`, which must be within an ARIA `role="row"` (if the ARIA grid is not making use of the native HTML `<table>` element and structure).
3.  Header cells and data cell association: Identify all column and row headers for each data cell. Check that all data cells are programmatically associated with relevant headers using one of the following techniques [SC 1.3.1]:
    -   For a simple HTML `<table>`, with all headers in the first row OR column, each header cell can be marked up with `<th>` without additional attributes.
    -   For any HTML `<table>`, header cells can be marked up with `<scope>` if all data cells that follow the header belong to the header. In HTML4, `<td scope>` is supported. In HTML5, `<td scope>` is not supported so all header cells must be `<th>`. Acceptable values for `scope` are `col|row|colgroup|rowgroup`. The `scope` only applies to cells that occur after the header cell(s) in the reading order.
    -   For any HTML `<table>`, data cells can be associated to a header cell by including the header cell's unique id value in `<td headers>`.
        -   Data cells must refer to the id(s) of all relevant header cells via the headers attribute in order for the row and column headers to be properly associated.
        -   The order of the IDs referenced in the headers attribute are consistent and in a meaningful sequence.
    -   For any HTML `<table>` that uses BOTH `<scope>` AND refers to header IDs using `<td headers>` attributes in the same table, any data cell with a `headers` reference will override any `scope` attributes for associated table headers for that particular data cell. Therefore, data cells with a `headers` reference, must identify all relevant headers, independent from and regardless of `scope` attributes in associated headers.
    -   For ARIA `role="table"`: each column header must have `role="columnheader"` and each row header must have `role="rowheader"`.
    -   For ARIA `role="grid"`: each column header must have `role="columnheader"` and each row header must have `role="rowheader"` (if the ARIA grid is not making use of the native HTML `<table>` element and structure).

### Test Results
If any of the above tests fail, Baseline Test 12.1-DataTable fails.

12.2 Test Procedure for Layout Tables
------------------------------------------------
**Baseline Test ID:** 12.2-LayoutTable
### Identify Content
All content/data visually presented in a table that retains any meanigful sequence when linearized.

Note: Linearization of table content is the presentation of a table’s two-dimensional content in one-dimensional order of the content in the source, beginning with the first cell in the first row and ending with the last cell in the last row, from left to right, top to bottom.

### Test Instructions
1.  Check that tables used purely for layout purposes [SC 1.3.1]:
    1.  Do NOT designate the layout as a table using ARIA role="table" and associated ARIA table attributes.
    2.  Do NOT include table structure and relationship elements and/or associated attributes (e.g, `<th>`, summary, `<caption>`, `scope`, and/or `headers`) UNLESS at least one of the following is true:
        * the table has `role="presentation"`
        * the table has `role="none"`
    3.  Do NOT identify column or row headers using `role="columnheader"` or `role="rowheader"` in an ARIA grid (where the data grid is identified using `role="grid"`).

### Test Results
If any of the above tests fail, Baseline Test 12.2-LayoutTable fails.

Advisory: Tips for streamlined test processes
---------------------------------------------
Content that is presented with a CSS table appearance, but does not rely on header association, can most easily be identified by linearization. Another helpful indicator is the table only has row headers or column headers but not both.

### WCAG 2.0 Techniques
The following sufficient techniques were considered when developing this test procedure for this baseline requirement:
-   [H43: Using id and headers attributes to associate data cells with header cells in data tables](https://www.w3.org/TR/WCAG20-TECHS/H43.html)
-   [H51: Using table markup to present tabular information](https://www.w3.org/TR/WCAG20-TECHS/H51.html)
-   [H63: Using the scope attribute to associate header cells and data cells in data tables](https://www.w3.org/TR/WCAG20-TECHS/H63.html)
-   [F49: Failure of Success Criterion 1.3.2 due to using an HTML layout table that does not make sense when linearized](https://www.w3.org/TR/WCAG20-TECHS/F49.html)
-   [F46: Failure of Success Criterion 1.3.1 due to using th elements, caption elements, or non-empty summary attributes in layout tables](http://www.w3.org/TR/WCAG20-TECHS/F46.html)

----------------------------------------
[Home/Table of Contents](index.md) | [Previous Baseline](11PageTitles.md) | [Next Baseline](13Structure.md)
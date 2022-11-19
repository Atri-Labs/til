# How to add a table in GitHub Flavored Markdown?
 
## Syntax

- Use pipes `|` to separate each column.
- Use hyphens `---` to create each column's header. 

To generate the following table, 

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |

use the following syntax:
```
| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |
```

Note:
- For column header, we need to add a minimum of three hyphens. 
- Cell widths can appear to vary in Markdown. However, the rendered output will look the same as above.

```
| Syntax | Description |
| --- | ----------- |
| Header | Title |
| Paragraph | Text |
```

## How to align text in a column?

Modify the header row as follows:

```
| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| git status   | git status     | git status    |
| git diff     | git diff       | git diff      |
```

| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| git status   | git status     | git status    |
| git diff     | git diff       | git diff      |

# QGridLayout

[← back](../qt-layouts.md)

Use `QGridLayout` when controls need to share row and column boundaries, such as labels and input fields.

```cpp
#include <QGridLayout>
#include <QHBoxLayout>
#include <QLabel>
#include <QLineEdit>
#include <QPushButton>
#include <QWidget>
```

## Summary

- [Cells and spans](#cells-and-spans)
- [Row and column sizes](#row-and-column-sizes)
- [Margins, spacing, and alignment](#margins-spacing-and-alignment)
- [Nested layouts](#nested-layouts)

## Cells and spans

`addWidget()` has separate forms for a single cell and for a rectangular span of cells:

```cpp
grid->addWidget(widget, row, column);
grid->addWidget(widget, row, column, rowSpan, columnSpan);
```

| Parameter | Meaning |
|---|---|
| `widget` | The widget to add |
| `row` | Starting row index, counted from `0` |
| `column` | Starting column index, counted from `0` |
| `rowSpan` | Number of rows occupied, starting at `row` |
| `columnSpan` | Number of columns occupied, starting at `column` |

The coordinates come first: **row, then column**. The spans follow: **row count, then column count**. The single-cell form occupies one row and one column. Spans are counts, not ending indices.

Both forms also accept an optional final `Qt::Alignment` argument; see [Margins, spacing, and alignment](#margins-spacing-and-alignment).

Passing `panel` to the layout constructor installs its top-level layout:

```cpp
QWidget *panel = new QWidget();
QGridLayout *grid = new QGridLayout(panel);

grid->addWidget(new QLabel("Name:"), 0, 0);
grid->addWidget(new QLineEdit(), 0, 1);
grid->addWidget(new QLabel("Email:"), 1, 0);
grid->addWidget(new QLineEdit(), 1, 1);

// widget, row, column, rowSpan, columnSpan
grid->addWidget(new QPushButton("Save"), 2, 0, 1, 2);
```

```text
          column 0   column 1
row 0     Name:      [             ]
row 1     Email:     [             ]
row 2     [         Save           ]
```

For the Save button, `2, 0` are the starting coordinates (row `2`, column `0`), and `1, 2` are the spans (one row, two columns). It occupies cells `(2, 0)` and `(2, 1)`.

## Row and column sizes

Rows and columns need not have equal sizes. Set stretch on the row or column, rather than on `addWidget()`.

| Function | Parameters and effect |
|---|---|
| `setColumnStretch(column, stretch)` | `column`: zero-based column index; `stretch`: non-negative relative factor for distributing extra width |
| `setRowStretch(row, stretch)` | `row`: zero-based row index; `stretch`: non-negative relative factor for distributing extra height |
| `setColumnMinimumWidth(column, minSize)` | `column`: zero-based column index; `minSize`: minimum column width in pixels |
| `setRowMinimumHeight(row, minSize)` | `row`: zero-based row index; `minSize`: minimum row height in pixels |

Stretch factors are proportions, not pixel sizes. For example, factors `1` and `2` give the second column twice the relative weight when distributing extra width. Minimum sizes are lower bounds, not fixed sizes; widget constraints can require larger rows or columns.

For example:

```cpp
grid->setColumnStretch(0, 0);
grid->setColumnStretch(1, 1); // give input fields extra width
grid->setColumnMinimumWidth(0, 80);

grid->setRowMinimumHeight(3, 12);
grid->setRowStretch(3, 1); // empty row absorbs extra height
```

Stretch is relative; widget size constraints still apply. Zero stretch does not fix a column's width.

## Margins, spacing, and alignment

The grid can use different gaps horizontally and vertically:

| Function | Parameter and effect |
|---|---|
| `setHorizontalSpacing(spacing)` | `spacing`: gap in pixels between neighboring columns |
| `setVerticalSpacing(spacing)` | `spacing`: gap in pixels between neighboring rows |

These gaps are inside the grid. For space around its edges, use `setContentsMargins(left, top, right, bottom)`, described in [Contents margins](space-distribution.md#contents-margins).

The optional final `alignment` argument of `addWidget()` accepts `Qt::Alignment` flags, such as `Qt::AlignRight` or `Qt::AlignRight | Qt::AlignVCenter`. It positions the widget within its allocated area. In the single-cell form below, `4, 1` are row and column, and `Qt::AlignRight` is the alignment.

```cpp
grid->setContentsMargins(12, 12, 12, 12);
grid->setHorizontalSpacing(8);
grid->setVerticalSpacing(6);

grid->addWidget(new QPushButton("Help"), 4, 1, Qt::AlignRight);
```

Alignment positions an item within its allocated area. See [Space allocation, margins, and spacing](space-distribution.md) for size policies and margins.

## Nested layouts

Use `addLayout()` to place a layout in a cell or span. Its coordinates and spans follow the same order as `addWidget()`:

```cpp
grid->addLayout(layout, row, column);
grid->addLayout(layout, row, column, rowSpan, columnSpan);
```

`layout` is the child layout to add; `row` and `column` are its zero-based starting coordinates. `rowSpan` and `columnSpan` count the rows and columns it occupies. Both forms accept an optional final `alignment` argument with the same meaning as for `addWidget()`.

The nested `QHBoxLayout` uses `addStretch()`, already covered in [Fixed and expanding empty space](space-distribution.md#fixed-and-expanding-empty-space).

For example, place the actions layout at row `5`, column `0`, spanning one row and two columns:

```cpp
QHBoxLayout *actions = new QHBoxLayout();
grid->addLayout(actions, 5, 0, 1, 2);
actions->addStretch();
actions->addWidget(new QPushButton("Cancel"));
actions->addWidget(new QPushButton("OK"));
```

The examples extend the same `grid`. Nested layouts have no widget parent argument.

Reference: [Qt documentation: QGridLayout](https://doc.qt.io/qt-6/qgridlayout.html).

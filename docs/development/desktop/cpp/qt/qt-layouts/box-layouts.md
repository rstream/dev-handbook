# QHBoxLayout and QVBoxLayout

[← back](../qt-layouts.md)

`QHBoxLayout` arranges items from left to right. `QVBoxLayout` arranges items from top to bottom. Both inherit `QBoxLayout` and use the same methods.

```cpp
#include <QHBoxLayout>
#include <QPushButton>
#include <QVBoxLayout>
#include <QWidget>
```

## Summary

- [Horizontal layout](#horizontal-layout)
- [Vertical layout](#vertical-layout)
- [Nested layouts](#nested-layouts)
- [Adding and inserting items](#adding-and-inserting-items)
- [Ownership](#ownership)
- [Notes](#notes)

## Horizontal layout

Pass the container to the layout constructor to install the layout on that widget.

```cpp
QWidget *panel = new QWidget();
QHBoxLayout *layout = new QHBoxLayout(panel);

layout->addWidget(new QPushButton("Back"));
layout->addWidget(new QPushButton("Next"));
```

The buttons form one horizontal row. The layout recalculates their geometry when `panel` is resized.

## Vertical layout

```cpp
QWidget *panel = new QWidget();
QVBoxLayout *layout = new QVBoxLayout(panel);

layout->addWidget(new QPushButton("Start"));
layout->addWidget(new QPushButton("Settings"));
layout->addWidget(new QPushButton("Exit"));
```

The buttons form one vertical column.

## Nested layouts

A layout can contain other layouts. Use this to combine rows and columns.

```cpp
QWidget *panel = new QWidget();
QVBoxLayout *mainLayout = new QVBoxLayout(panel);

QHBoxLayout *toolbarLayout = new QHBoxLayout();
toolbarLayout->addWidget(new QPushButton("Open"));
toolbarLayout->addWidget(new QPushButton("Save"));

QHBoxLayout *actionsLayout = new QHBoxLayout();
actionsLayout->addWidget(new QPushButton("Cancel"));
actionsLayout->addWidget(new QPushButton("OK"));

mainLayout->addLayout(toolbarLayout);
mainLayout->addLayout(actionsLayout);
```

Here `mainLayout` divides the container vertically between two child layouts. Each child layout distributes its own area horizontally between its widgets.

## Adding and inserting items

Append items to the end of a layout:

```cpp
layout->addWidget(button);
layout->addLayout(childLayout);
```

Insert items at a specific position:

```cpp
layout->insertWidget(0, button);
layout->insertLayout(1, childLayout);
```

Remove an item from layout management without deleting it:

```cpp
layout->removeWidget(button);
```

## Ownership

Installing a layout on a widget makes it the widget's top-level layout. Widgets added to that layout are reparented to the layout's container widget.

Nested layouts are owned through the top-level layout. A layout itself is not a visual widget and does not become the parent of added widgets.

## Notes

* Do not install more than one top-level layout on the same widget.
* Use `addLayout()` instead of trying to add a layout with `addWidget()`.
* Space allocation is affected by size policies and stretch factors; see [Space allocation, margins, and spacing](space-distribution.md).

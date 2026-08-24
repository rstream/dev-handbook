# Space allocation, margins, and spacing

[← back](../qt-layouts.md)

A box layout first satisfies item size constraints and then distributes the available space according to size policies, stretch factors, alignment, and spacer items.

```cpp
#include <QBoxLayout>
#include <QMargins>
#include <QSizePolicy>
```

In a `QHBoxLayout`, stretch factors and spacer items distribute horizontal space. In a `QVBoxLayout`, they distribute vertical space. Size policies still apply independently in both directions.

## Summary

- [Empty space controls](#empty-space-controls)
- [How widget size is determined](#how-widget-size-is-determined)
- [Space allocation between widgets](#space-allocation-between-widgets)
- [Space allocation between child layouts](#space-allocation-between-child-layouts)
- [Changing stretch factors](#changing-stretch-factors)
- [Fixed and expanding empty space](#fixed-and-expanding-empty-space)
- [Alignment](#alignment)
- [Common patterns](#common-patterns)

## Empty space controls

Do not confuse margins, spacing, and explicit spacer items:

| Mechanism | Where the empty space appears | Scope |
|---|---|---|
| `setContentsMargins()` | Between the layout boundary and its outermost items | All four edges |
| `setSpacing()` | Between neighboring items managed by the layout | Every neighboring pair |
| `addSpacing()` | At the exact position where it was added | One fixed-size spacer |
| `addStretch()` | At the exact position where it was added | One expanding spacer |

### Contents margins

Contents margins are the empty area between the layout's boundary and its managed items. For a top-level layout, these are internal margins along the inside edge of the container widget. They are not external margins outside the widget.

```cpp
layout->setContentsMargins(12, 8, 12, 8);
// left, top, right, bottom
```

These are not margins inside the child widgets. A widget can have its own content margins, independent of the layout.

Read the current values when needed:

```cpp
QMargins margins = layout->contentsMargins();
```

### Spacing between adjacent items

`spacing` is the default gap inserted between every pair of adjacent items in that layout.

```cpp
layout->setSpacing(6);
```

The argument is the gap size in pixels.

It does not add space before the first item or after the last item. Use contents margins for the edges.

### Explicit spacer items

`addSpacing()` and `addStretch()` add an item at one exact position in the row or column. They do not change the default gap between all items.

```cpp
layout->addWidget(firstButton);
layout->addSpacing(20);  // fixed 20-pixel empty item here
layout->addWidget(secondButton);
layout->addStretch();    // expanding empty item after the buttons
```

## How widget size is determined

The layout considers several properties of every widget:

* `minimumSize` and `minimumSizeHint()` limit how small it should become.
* `sizeHint()` provides its preferred size.
* `maximumSize` limits how large it can become.
* `QSizePolicy` tells the layout whether the widget can shrink or expand horizontally and vertically.
* A stretch factor determines its share of space relative to sibling items.

For example, make a text editor expand while a button stays near its preferred size:

```cpp
editor->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);
button->setSizePolicy(QSizePolicy::Fixed, QSizePolicy::Fixed);
```

Size policy and stretch solve different parts of the problem: the policy describes what a widget is allowed or expected to do, while stretch describes its relative share in a particular layout.

## Space allocation between widgets

`addWidget()` accepts the widget followed by its stretch factor:

```cpp
QHBoxLayout *layout = new QHBoxLayout(panel);
layout->addWidget(leftWidget, 1);  // widget, stretch factor
layout->addWidget(rightWidget, 2); // widget, stretch factor
```

The first argument identifies the widget being added. The second argument is its relative stretch factor within this layout.

Subject to their minimum, maximum, size hint, and size policy, `rightWidget` receives approximately twice the stretchable space of `leftWidget`.

A stretch factor of `0` does not mean zero width or height. It means the item does not claim a proportional share through a positive stretch factor; its size policy and size hints still apply.

## Space allocation between child layouts

`addLayout()` accepts the child layout followed by its stretch factor:

```cpp
QHBoxLayout *mainLayout = new QHBoxLayout(panel);
mainLayout->addLayout(navigationLayout, 1); // child layout, stretch factor
mainLayout->addLayout(contentLayout, 3);    // child layout, stretch factor
```

The first argument identifies the child layout. The second argument is its relative stretch factor within `mainLayout`.

The top-level layout assigns space to the two child layouts in an approximate `1:3` ratio, subject to the constraints of the items inside them. Each child layout then distributes its assigned area among its own widgets.

Stretch factors at one level do not directly control items inside another level:

```text
mainLayout:       navigationLayout (1) | contentLayout (3)
                                           │
contentLayout:                         editor (4) | preview (1)
```

The first ratio divides space between the child layouts. The second ratio divides the content layout's area between its widgets.

## Changing stretch factors

Use `setStretch(index, stretch)` when items have already been added:

```cpp
layout->addWidget(leftWidget);
layout->addWidget(rightWidget);

layout->setStretch(0, 1); // item index 0, stretch factor 1
layout->setStretch(1, 2); // item index 1, stretch factor 2
```

* `index` is the zero-based position of an item in this layout. Widgets, child layouts, and spacer items all occupy positions.
* `stretch` is the relative stretch factor assigned to that item.

`setStretchFactor(item, stretch)` can avoid depending on an index. Its first argument is a widget or child layout, and its second argument is the new stretch factor:

```cpp
layout->setStretchFactor(leftWidget, 1);
layout->setStretchFactor(rightWidget, 2);
```

It also accepts a child layout:

```cpp
layout->setStretchFactor(sidebarLayout, 1);
layout->setStretchFactor(contentLayout, 3);
```

## Fixed and expanding empty space

Use a fixed spacer when the gap must have a specific size:

```cpp
layout->addWidget(label);
layout->addSpacing(12);
layout->addWidget(input);
```

The argument of `addSpacing(size)` is the fixed spacer size in pixels.

Use a stretchable spacer to consume remaining space:

```cpp
layout->addWidget(cancelButton);
layout->addStretch(1);
layout->addWidget(okButton);
```

The optional argument of `addStretch(stretch)` is the spacer's relative stretch factor. It defaults to `0`.

In a horizontal layout, the spacer expands horizontally. In a vertical layout, it expands vertically.

Multiple stretches divide available empty space proportionally:

```cpp
layout->addStretch(1);
layout->addWidget(button);
layout->addStretch(1); // centers the button between equal stretches
```

## Alignment

Alignment controls where an item is placed inside the area assigned to it. It does not replace stretch factors.

```cpp
layout->addWidget(button, 0, Qt::AlignRight | Qt::AlignVCenter);
```

The arguments are the widget, its stretch factor, and its alignment flags. Here the button has no positive stretch factor and is aligned to the right and vertically centered inside its assigned area.

Without an alignment flag, the layout normally lets the widget fill its assigned area in permitted directions. With alignment, the widget can remain near its size hint and be positioned within that area.

## Common patterns

### Equal-width widgets

```cpp
layout->addWidget(firstWidget, 1);
layout->addWidget(secondWidget, 1);
layout->addWidget(thirdWidget, 1);
```

This produces equal shares when widget constraints allow it.

### Fixed controls followed by expanding content

```cpp
layout->addWidget(label, 0);
layout->addWidget(editor, 1);
```

The label stays near its preferred width and the editor receives the remaining stretchable space.

### Controls aligned to the right

```cpp
layout->addStretch();
layout->addWidget(cancelButton);
layout->addWidget(okButton);
```

The stretchable spacer consumes free space before the buttons and pushes them to the right.

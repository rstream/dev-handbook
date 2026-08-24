# QGroupBox

[← back](../qt-widgets.md)

`QGroupBox` is a container widget that visually groups related controls inside a frame with an optional title. It inherits `QWidget`; it is not a layout.

```cpp
#include <QGroupBox>
#include <QLabel>
#include <QLineEdit>
#include <QVBoxLayout>
```

## Summary

- [Basic usage](#basic-usage)
- [Title and alignment](#title-and-alignment)
- [Checkable group](#checkable-group)
- [Flat group](#flat-group)
- [Signals](#signals)
- [QGroupBox and QButtonGroup](#qgroupbox-and-qbuttongroup)
- [Notes](#notes)

## Basic usage

`QGroupBox` draws the group, but does not arrange its children automatically. Install a layout on the group box and add the child widgets to that layout.

```cpp
QGroupBox *connectionGroup = new QGroupBox("Connection");
QVBoxLayout *groupLayout = new QVBoxLayout(connectionGroup);

groupLayout->addWidget(new QLabel("Server address:"));
groupLayout->addWidget(new QLineEdit());

mainLayout->addWidget(connectionGroup);
```

Here `groupLayout` manages the controls inside `connectionGroup`. `mainLayout` only allocates an area for the complete group box among the other widgets in the window.

## Title and alignment

Set or read the title:

```cpp
connectionGroup->setTitle("Network connection");
QString title = connectionGroup->title();
```

Align the title inside the group box header:

```cpp
connectionGroup->setAlignment(Qt::AlignHCenter);
```

The argument is a horizontal alignment flag. Common values are `Qt::AlignLeft`, `Qt::AlignHCenter`, and `Qt::AlignRight`.

Use `&` to assign a keyboard mnemonic:

```cpp
QGroupBox *connectionGroup = new QGroupBox("&Connection");
```

## Checkable group

A checkable group box displays a checkbox in its title. Unchecking it disables the child controls; checking it enables them again.

```cpp
connectionGroup->setCheckable(true);
connectionGroup->setChecked(false);
```

`setCheckable(bool)` controls whether the title has a checkbox. `setChecked(bool)` controls its state.

Child widgets that were explicitly disabled remain disabled when the group is checked again.

## Flat group

Flat mode reduces the visual frame around the group:

```cpp
connectionGroup->setFlat(true);
```

Use it when the title is useful but a complete frame would add too much visual weight.

## Signals

Track any change of the checked state:

```cpp
QObject::connect(connectionGroup, &QGroupBox::toggled, [](bool checked) {
    // checked is the new group state
});
```

* `toggled(bool checked)` is emitted when the checked state changes programmatically or through user interaction.
* `clicked(bool checked)` is emitted when the user activates the group box checkbox.

These signals are relevant when `setCheckable(true)` is enabled.

## QGroupBox and QButtonGroup

The classes have different purposes:

| Class | Visible | Purpose |
|---|---|---|
| `QGroupBox` | Yes | Draws a titled container for related widgets |
| `QButtonGroup` | No | Manages logical relationships and IDs for buttons |

They can be used together: `QGroupBox` provides the visual section, while `QButtonGroup` manages the buttons inside it.

Radio buttons that share the same parent are auto-exclusive by default. Placing each set in a separate `QGroupBox` also gives each set a separate parent and therefore a separate auto-exclusive scope.

## Notes

* Use a layout such as [QHBoxLayout or QVBoxLayout](../qt-layouts/box-layouts.md) to arrange child widgets inside the group box.
* Add the complete `QGroupBox` to its parent layout with `addWidget()`.
* Use a plain `QWidget` when a container does not need a visible title or frame.

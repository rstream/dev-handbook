# Widget fonts and QFont

[← back](../qt-widgets.md)

`QFont` describes a font. `QWidget::setFont()` applies it to a widget, so the same method is available to `QLabel`, `QPushButton`, `QLineEdit`, `QGroupBox`, and other `QWidget`-based controls.

```cpp
#include <QApplication>
#include <QFont>
#include <QWidget>
```

## Summary

- [Basic usage](#basic-usage)
- [Modifying the current font](#modifying-the-current-font)
- [Common font properties](#common-font-properties)
- [Point size and pixel size](#point-size-and-pixel-size)
- [Font inheritance](#font-inheritance)
- [Application font](#application-font)
- [Notes](#notes)

## Basic usage

Create a font, set its properties, and assign it to a widget:

```cpp
QFont font;
font.setFamily("Noto Sans");
font.setPointSize(12);
font.setBold(true);

widget->setFont(font);
```

`setFont(const QFont &font)` takes the font that should be applied to the widget. If the requested family is unavailable, Qt selects a suitable replacement.

Read the widget's current font with `font()`:

```cpp
QFont font = widget->font();
```

## Modifying the current font

Copy the current font when only one or two properties need to change. This preserves its other settings:

```cpp
QFont font = widget->font();
font.setPointSize(14);
font.setItalic(true);

widget->setFont(font);
```

Calling `widget->font()` does not return a reference that can be modified in place. Change the copied `QFont`, then pass it back to `setFont()`.

## Common font properties

```cpp
font.setFamily("Noto Sans");
font.setPointSize(12);
font.setWeight(QFont::DemiBold);
font.setItalic(true);
font.setUnderline(true);
font.setStrikeOut(false);
```

| Method | Parameter |
|---|---|
| `setFamily(family)` | Font family name |
| `setPointSize(size)` | Size in points |
| `setPixelSize(size)` | Size in pixels |
| `setWeight(weight)` | A `QFont::Weight` value such as `Normal`, `DemiBold`, or `Bold` |
| `setBold(enabled)` | Enables or disables bold weight |
| `setItalic(enabled)` | Enables or disables italic style |
| `setUnderline(enabled)` | Enables or disables underlining |
| `setStrikeOut(enabled)` | Enables or disables strikeout |

Read properties through the corresponding getters:

```cpp
QString family = font.family();
int pointSize = font.pointSize();
bool bold = font.bold();
bool italic = font.italic();
```

## Point size and pixel size

Point size is device-independent and normally preferred for user-interface text:

```cpp
font.setPointSize(12);
```

Pixel size requests a particular pixel height and is useful when text must match pixel-based graphics:

```cpp
font.setPixelSize(16);
```

Choose one size unit for a font. After `setPixelSize()`, `pointSize()` returns `-1`; after `setPointSize()`, `pixelSize()` returns `-1`.

## Font inheritance

Fonts propagate from a parent widget to its children. Set a font on a container when all controls inside it should use the same font:

```cpp
QFont panelFont = panel->font();
panelFont.setPointSize(12);
panel->setFont(panelFont);
```

Child widgets inherit the explicitly changed font properties unless they override them with their own `setFont()` call.

## Application font

Set the default font for the complete application with `QApplication::setFont()`:

```cpp
QFont appFont = QApplication::font();
appFont.setFamily("Noto Sans");
appFont.setPointSize(11);

QApplication::setFont(appFont);
```

Set the application font before creating the widgets when possible. Use `widget->setFont()` afterwards only for controls that need a local override.

## Notes

* `setFont()` changes presentation, not the widget's text or content.
* Avoid relying on a font family that may not be installed on the target system.
* Widget styles can adjust the final rendered font to match the platform.
* Mixing `setFont()` with font rules in Qt style sheets can make inheritance harder to follow; prefer one approach for a given part of the interface.

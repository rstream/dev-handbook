# QLabel

[← back](../qt-widgets.md)

`QLabel` displays read-only text or an image. Use it for captions, field labels, status text, and short messages inside a form.

```cpp
#include <QLabel>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Rich text](#rich-text)
- [Notes](#notes)

## Basic usage

```cpp
QLabel *label = new QLabel("Sample text");

QString text = label->text();
text += " gets longer...";
label->setText(text);

layout->addWidget(label);
```

## Common operations

```cpp
label->setWordWrap(true);
label->setAlignment(Qt::AlignCenter);
label->setText("Updated text");
label->clear();
```

If you are using `setWordWrap` (multiline label) - define size policy to make sure widget will not take more vertical space than it needs:
```cpp
label->setSizePolicy(QSizePolicy::Preferred, QSizePolicy::Preferred);
```
Read more about [Size policies](../qt-layouts/space-distribution.md).

## Rich text

`QLabel` can render simple rich text automatically when the text looks like HTML.

```cpp
QLabel *label = new QLabel("<b>Status:</b> ready");
label->setOpenExternalLinks(true);
```

## Notes

* `QLabel` is not editable. Use `QLineEdit`, `QPlainTextEdit`, or `QTextEdit` for user input.
* Long text usually needs `setWordWrap(true)`.
* For a label linked to an input field, use `setBuddy()`.

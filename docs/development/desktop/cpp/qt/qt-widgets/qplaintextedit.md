# QPlainTextEdit

[← back](../qt-widgets.md)

`QPlainTextEdit` is a multi-line editor for plain text. It is a good choice for logs, source text, notes, and other content that does not need formatting.

```cpp
#include <QPlainTextEdit>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Signals](#signals)
- [Notes](#notes)

## Basic usage

```cpp
QPlainTextEdit *plainTextEdit = new QPlainTextEdit();
plainTextEdit->setFixedHeight(64);

QObject::connect(plainTextEdit, &QPlainTextEdit::textChanged, [plainTextEdit]() {
	if (plainTextEdit->toPlainText() == "42") {
		plainTextEdit->setPlainText("Sense of being");
	}
});

layout->addWidget(plainTextEdit);
```

## Common operations

```cpp
plainTextEdit->setPlainText("Line 1\nLine 2");
plainTextEdit->appendPlainText("Line 3");

QString text = plainTextEdit->toPlainText();
plainTextEdit->clear();
plainTextEdit->setReadOnly(true);
```

## Signals

* `textChanged()` is emitted when the document content changes.
* Use `QTextCursor` when you need precise cursor or selection control.

## Notes

* Use `QPlainTextEdit` for plain text and large text blocks.
* Use `QTextEdit` when rich text or HTML formatting is needed.

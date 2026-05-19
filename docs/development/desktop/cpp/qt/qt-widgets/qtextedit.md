# QTextEdit

[← back](../qt-widgets.md)

`QTextEdit` is a multi-line editor for rich text. It can display and edit formatted text, HTML snippets, and plain text.

```cpp
#include <QFont>
#include <QTextEdit>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Formatting](#formatting)
- [Signals](#signals)
- [Notes](#notes)

## <a id="basic-usage"></a>Basic usage

```cpp
QTextEdit *textEdit = new QTextEdit();
textEdit->setFixedHeight(64);

QObject::connect(textEdit, &QTextEdit::textChanged, [textEdit]() {
	if (textEdit->toPlainText() == "disable") {
		textEdit->setDisabled(true);
	}
});

layout->addWidget(textEdit);
```

## <a id="common-operations"></a>Common operations

```cpp
textEdit->setPlainText("Plain text");
textEdit->setHtml("<b>Rich text</b>");

QString plain = textEdit->toPlainText();
QString html = textEdit->toHtml();

textEdit->clear();
textEdit->setReadOnly(true);
```

## <a id="formatting"></a>Formatting

```cpp
textEdit->setAcceptRichText(true);
textEdit->setFontItalic(true);
textEdit->setFontWeight(QFont::Bold);
```

## <a id="signals"></a>Signals

* `textChanged()` is emitted when the document content changes.
* `copyAvailable(bool)` is emitted when text selection becomes available or unavailable.

## <a id="notes"></a>Notes

* Use `QTextEdit` for rich text and HTML.
* Use `QPlainTextEdit` for logs, code, or large plain text content.

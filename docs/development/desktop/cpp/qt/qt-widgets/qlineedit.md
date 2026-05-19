# QLineEdit

[← back](../qt-widgets.md)

`QLineEdit` is a single-line text input. Use it for names, paths, filters, search boxes, passwords, and short values.

```cpp
#include <QLineEdit>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Password input](#password-input)
- [Signals](#signals)
- [Notes](#notes)

## <a id="basic-usage"></a>Basic usage

```cpp
QLineEdit *lineEdit = new QLineEdit("John");
lineEdit->setMaxLength(20);
lineEdit->setPlaceholderText("enter name");

QObject::connect(lineEdit, &QLineEdit::textEdited, [](QString text) {
	cout << text.toStdString() << endl;
});

layout->addWidget(lineEdit);
```

## <a id="common-operations"></a>Common operations

```cpp
QString text = lineEdit->text();
lineEdit->setText(text + " Doe");
lineEdit->clear();
lineEdit->setReadOnly(true);
lineEdit->setDisabled(true);
```

## <a id="password-input"></a>Password input

```cpp
lineEdit->setEchoMode(QLineEdit::Password);
```

## <a id="signals"></a>Signals

* `textEdited(QString)` is emitted only when the user edits the text.
* `textChanged(QString)` is emitted for both user edits and programmatic `setText()`.
* `returnPressed()` is emitted when the user presses Enter.

## <a id="notes"></a>Notes

* `setReadOnly(true)` keeps the field selectable and focusable.
* `setDisabled(true)` grays out the field and removes normal interaction.

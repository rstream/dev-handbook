# QPlainTextEdit

[← back](../qt-widgets.md)

Multi-line plain text box

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
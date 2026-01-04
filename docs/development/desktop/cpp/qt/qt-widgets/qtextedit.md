# QTextEdit

[← back](../qt-widgets.md)

Multi-line rich text box

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
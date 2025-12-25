# QLineEdit

[← back](../qt-widgets.md)

Display single-line text input field

```cpp
QLineEdit *lineEdit = new QLineEdit("John");
// max length
lineEdit->setMaxLength(20);
// placeholder
lineEdit->setPlaceholderText("enter name");
// get text
QString text = lineEdit->text();
text += " Doe";
// set text
lineEdit->setText(text);
// text change event
QObject::connect(lineEdit, &QLineEdit::textEdited, [lineEdit](QString text) {
	cout << text.toStdString() << endl;
	if (text == "John Doe.") {
		// set  disabled (gray)
		lineEdit->setDisabled(true);
	}
	if (text == "John Doe,") {
		// set read only
		lineEdit->setReadOnly(true);
	}
});
layout->addWidget(lineEdit);
```
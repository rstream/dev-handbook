# QLabel

[← back](../qt-widgets.md)

Display static text label

```cpp
QLabel *label = new QLabel("Sample text");
// get text
QString text = label->text();
text += " gets longer...";
// set text
label->setText(text);
layout->addWidget(label);
```
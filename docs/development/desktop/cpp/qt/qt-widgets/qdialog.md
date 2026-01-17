# QDialog

[← back](../qt-widgets.md)

Custom Dialog window

```cpp
QDialog *dlg = new QDialog(win);
dlg->setWindowTitle("Dialog");
dlg->setFixedWidth(300);
QVBoxLayout *layout = new QVBoxLayout(dlg);
QLabel *label = new QLabel("Sample dialog window ade using QDialog. Blocks parent window intil close.");
label->setWordWrap(true);
label->setAlignment(Qt::AlignJustify);
QPushButton *button = new QPushButton("OK");
layout->addWidget(label);
layout->addWidget(button, 0, Qt::AlignHCenter);
QObject::connect(button, &QPushButton::clicked, [dlg]() {
	dlg->close();
});
dlg->exec();
```
# QDialog

[← back](../index.md)

`QDialog` is a custom dialog window. Use it when `QMessageBox` is too limited and you need your own layout, inputs, and buttons.

```cpp
#include <QDialog>
#include <QDialogButtonBox>
#include <QLabel>
#include <QPushButton>
#include <QVBoxLayout>
```

## Basic usage

```cpp
QDialog *dlg = new QDialog(win);
dlg->setWindowTitle("Dialog");
dlg->setFixedWidth(300);

QVBoxLayout *layout = new QVBoxLayout(dlg);
QLabel *label = new QLabel("Sample dialog window made using QDialog.");
label->setWordWrap(true);
label->setAlignment(Qt::AlignJustify);

QPushButton *button = new QPushButton("OK");
layout->addWidget(label);
layout->addWidget(button, 0, Qt::AlignHCenter);

QObject::connect(button, &QPushButton::clicked, [dlg]() {
	dlg->accept();
});

dlg->exec();
```

## Accept and reject

`exec()` returns `QDialog::Accepted` or `QDialog::Rejected`.

```cpp
QDialog dialog(win);
dialog.setWindowTitle("Confirm");

QVBoxLayout *layout = new QVBoxLayout(&dialog);
QLabel *label = new QLabel("Apply changes?");

QDialogButtonBox *buttons = new QDialogButtonBox(
    QDialogButtonBox::Ok | QDialogButtonBox::Cancel,
    &dialog
);

layout->addWidget(label);
layout->addWidget(buttons);

QObject::connect(buttons, &QDialogButtonBox::accepted, &dialog, &QDialog::accept);
QObject::connect(buttons, &QDialogButtonBox::rejected, &dialog, &QDialog::reject);

if (dialog.exec() == QDialog::Accepted) {
    // apply changes
}
```

## Modal and modeless

```cpp
dlg->exec(); // modal: blocks interaction with the parent window
dlg->show(); // modeless: opens and returns immediately
```

## Notes

* Use `accept()` for OK/Apply-like actions.
* Use `reject()` for Cancel/Close-like actions.
* Prefer `QMessageBox` for simple alerts and confirmations.

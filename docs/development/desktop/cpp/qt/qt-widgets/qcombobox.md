# QComboBox

[← back](../qt-widgets.md)

`QComboBox` is a dropdown for selecting one value from a list. It is best for short lists where only one option can be active.

```cpp
#include <QComboBox>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Item data](#item-data)
- [Signals](#signals)
- [Notes](#notes)

## Basic usage

```cpp
QComboBox *combo = new QComboBox();
combo->addItems({"Canada", "New Zealand", "Australia"});

QObject::connect(combo, &QComboBox::activated, [combo](int index) {
	cout << index << ": " << combo->currentText().toStdString() << endl;
});

layout->addWidget(combo);
```

## Common operations

```cpp
combo->addItem("Poland");
combo->insertItem(0, "Select country...");
combo->setCurrentIndex(0);

int index = combo->currentIndex();
QString text = combo->currentText();
```

## Item data

Each item can store hidden data in addition to visible text.

```cpp
combo->addItem("Canada", "CA");
combo->addItem("Poland", "PL");

QString countryCode = combo->currentData().toString();
```

## Signals

* `activated(int)` is emitted when the user selects an item.
* `currentIndexChanged(int)` is emitted when the current index changes, including programmatic changes.
* `currentTextChanged(QString)` is useful when the text matters more than the index.

## Notes

* Use `setEditable(true)` if the user should be able to type a custom value.
* Use item data for IDs/codes instead of parsing visible text.

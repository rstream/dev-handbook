# QListWidget

[← back](../qt-widgets.md)

`QListWidget` displays a list of items and manages item objects for you. It is convenient for simple lists; for large or data-driven lists, use `QListView` with a model.

```cpp
#include <QAbstractItemView>
#include <QListWidget>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Selection mode](#selection-mode)
- [Signals](#signals)
- [Notes](#notes)

## Basic usage

```cpp
QListWidget *list = new QListWidget();
list->setFixedHeight(100);
list->addItems({ "Katowice", "Sosnowiec", "Tychy" });

QObject::connect(list, &QListWidget::itemSelectionChanged, [list]() {
	auto *item = list->currentItem();
	if (item) {
		cout << item->text().toStdString() << endl;
	}
});

layout->addWidget(list);
```

## Common operations

```cpp
list->addItem("Gliwice");
list->setCurrentRow(0);

QListWidgetItem *item = list->currentItem();
int row = list->currentRow();

delete list->takeItem(row);
list->clearSelection();
```

## Selection mode

```cpp
list->setSelectionMode(QAbstractItemView::MultiSelection);
QList<QListWidgetItem *> items = list->selectedItems();
```

## Signals

* `itemClicked(QListWidgetItem *)` is emitted when the user clicks an item.
* `itemSelectionChanged()` is emitted when the selection changes.
* `currentRowChanged(int)` is convenient when only the row number is needed.

## Notes

* Check `currentItem()` for `nullptr` when the list may have no selection.
* `takeItem()` removes an item from the list but does not delete it.

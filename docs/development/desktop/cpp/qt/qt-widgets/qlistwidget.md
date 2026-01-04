# QListWidget

[← back](../qt-widgets.md)

List with selectable options

```cpp
QListWidget *list = new QListWidget();
list->setFixedHeight(100);
list->addItems({ "Katowice", "Sosnowiec", "Tychy" });
list->addItem("Ghost");
QObject::connect(list, &QListWidget::itemSelectionChanged, [list]() {
	auto *item = list->currentItem();
	cout << item->text().toStdString() << endl;
	if (item->text() == "Ghost") {
		int index = list->currentRow();
		delete list->takeItem(index);
		list->clearSelection();
	}
});
layout->addWidget(list);
```
# QComboBox

[← back](../qt-widgets.md)

Dropdown

```cpp
QComboBox *combo = new QComboBox();
combo->addItems({"", "Canada", "New Zealand", "Australia"});
combo->addItem("Nowhere");
QObject::connect(combo, &QComboBox::activated, [combo]() {
	if (combo->currentIndex() == 4) {
		combo->setCurrentIndex(0);
		combo->setDisabled(true);
	}
});
layout->addWidget(combo);
```
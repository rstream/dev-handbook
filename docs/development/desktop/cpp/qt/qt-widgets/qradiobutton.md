# QRadioButton

[← back](../qt-widgets.md)

**Grouped** radio buttons with text labels

```cpp
QButtonGroup *radios = new QButtonGroup();
QRadioButton *rad1 = new QRadioButton("Katowice");
QRadioButton *rad2 = new QRadioButton("Sosnowiec");
QRadioButton *rad3 = new QRadioButton("Nowhere");
// add buttons to group, assign IDs
radios->addButton(rad1, 1);
radios->addButton(rad2, 2);
radios->addButton(rad3, 3);
// toggle event
QObject::connect(radios, &QButtonGroup::buttonToggled, [radios](QAbstractButton *btn, bool checked) {
	if (checked) {
		// button from param
		cout << btn->text().toStdString() << endl;
		// button from QButtonGroup
		cout << radios->checkedButton()->text().toStdString() << endl;
		// get checked button ID
		if (radios->checkedId() == 3) {
			// set radio by ID
			radios->button(1)->setChecked(true);
		}
	}
});
layout->addWidget(rad1);
layout->addWidget(rad2);
layout->addWidget(rad3);
```
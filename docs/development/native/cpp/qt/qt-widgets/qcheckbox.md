# QCheckBox

[← back](../qt-widgets.md)

Checkbox with text label

```cpp
QCheckBox *checkbox = new QCheckBox("Check me!");
int counter = 1;
// custom property
checkbox->setProperty("counter", 0);
// get value
bool checked = checkbox->isChecked();
// set value
checkbox->setChecked(!checked);
// toggle event
QObject::connect(checkbox, &QCheckBox::toggled, [checkbox](bool checked) {
	int counter = checkbox->property("counter").toInt() + 1;
	checkbox->setProperty("counter", counter);
	cout << counter << " = " << (checked ? "on" : "off") << endl;
	if (counter > 5) {
		// disable
		checkbox->setDisabled(true);
	}
});
layout->addWidget(checkbox);
```
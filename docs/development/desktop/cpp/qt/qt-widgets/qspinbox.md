# QSpinbox

[← back](../qt-widgets.md)

Spinbox with top/down arrow buttons

```cpp
QSpinBox *spin = new QSpinBox();
spin->setRange(0, 100);
spin->setSingleStep(10);
spin->setSuffix("%");
spin->setValue(10);
QObject::connect(spin, &QSpinBox::valueChanged, [spin](int value) {
	cout << "V=" << value << endl;
	if (value == 100) {
		spin->setValue(0);
	}
});
layout->addWidget(spin);
```
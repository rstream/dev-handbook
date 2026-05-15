# QCheckBox

[← back](../qt-widgets.md)

`QCheckBox` is used for an independent on/off option. It is a good fit for settings that can be enabled or disabled separately.

```cpp
#include <QCheckBox>
```

## Basic usage

```cpp
QCheckBox *checkbox = new QCheckBox("Check me!");
checkbox->setChecked(true);

QObject::connect(checkbox, &QCheckBox::toggled, [](bool checked) {
	cout << (checked ? "on" : "off") << endl;
});

layout->addWidget(checkbox);
```

## Common operations

```cpp
bool checked = checkbox->isChecked();
checkbox->setChecked(!checked);
checkbox->setDisabled(true);
```

## Three states

Use tri-state mode when the checkbox can represent "partially checked".

```cpp
checkbox->setTristate(true);
checkbox->setCheckState(Qt::PartiallyChecked);
```

## Signals

* `toggled(bool)` is emitted when the checked state changes.
* `stateChanged(int)` is useful when tri-state mode is enabled.

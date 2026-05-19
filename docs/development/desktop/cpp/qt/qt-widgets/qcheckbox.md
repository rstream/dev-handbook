# QCheckBox

[← back](../qt-widgets.md)

`QCheckBox` is used for an independent on/off option. It is a good fit for settings that can be enabled or disabled separately.

```cpp
#include <QCheckBox>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Three states](#three-states)
- [Signals](#signals)

## <a id="basic-usage"></a>Basic usage

```cpp
QCheckBox *checkbox = new QCheckBox("Check me!");
checkbox->setChecked(true);

QObject::connect(checkbox, &QCheckBox::toggled, [](bool checked) {
	cout << (checked ? "on" : "off") << endl;
});

layout->addWidget(checkbox);
```

## <a id="common-operations"></a>Common operations

```cpp
bool checked = checkbox->isChecked();
checkbox->setChecked(!checked);
checkbox->setDisabled(true);
```

## <a id="three-states"></a>Three states

Use tri-state mode when the checkbox can represent "partially checked".

```cpp
checkbox->setTristate(true);
checkbox->setCheckState(Qt::PartiallyChecked);
```

## <a id="signals"></a>Signals

* `toggled(bool)` is emitted when the checked state changes.
* `stateChanged(int)` is useful when tri-state mode is enabled.

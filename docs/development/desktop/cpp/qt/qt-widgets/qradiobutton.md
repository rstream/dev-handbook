# QRadioButton

[← back](../qt-widgets.md)

`QRadioButton` is used when the user must select exactly one option from a small group. Use `QButtonGroup` when you want IDs or need to group buttons that do not share the same parent.

```cpp
#include <QButtonGroup>
#include <QRadioButton>
```

## Basic usage

```cpp
QButtonGroup *radios = new QButtonGroup();
QRadioButton *rad1 = new QRadioButton("Katowice");
QRadioButton *rad2 = new QRadioButton("Sosnowiec");
QRadioButton *rad3 = new QRadioButton("Nowhere");

radios->addButton(rad1, 1);
radios->addButton(rad2, 2);
radios->addButton(rad3, 3);

QObject::connect(radios, &QButtonGroup::buttonToggled, [radios](QAbstractButton *btn, bool checked) {
	if (checked) {
		cout << btn->text().toStdString() << endl;
		cout << "ID=" << radios->checkedId() << endl;
	}
});

layout->addWidget(rad1);
layout->addWidget(rad2);
layout->addWidget(rad3);
```

## Common operations

```cpp
rad1->setChecked(true);
QAbstractButton *button = radios->checkedButton();
int id = radios->checkedId();
radios->button(2)->setChecked(true);
```

## Signals

* `QRadioButton::toggled(bool)` tracks one button.
* `QButtonGroup::buttonToggled(QAbstractButton *, bool)` tracks the whole group.
* `QButtonGroup::idToggled(int, bool)` is convenient when you assigned IDs.

## Notes

* Radio buttons with the same parent are auto-exclusive by default.
* `QButtonGroup` is not visible. It only manages button relationships and IDs.

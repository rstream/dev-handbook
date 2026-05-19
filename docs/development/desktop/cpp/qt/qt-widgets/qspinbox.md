# QSpinBox

[← back](../qt-widgets.md)

`QSpinBox` is an integer input with arrow buttons. Use it when the value is numeric, bounded, and should be easy to adjust step by step.

```cpp
#include <QSpinBox>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Signals](#signals)
- [Notes](#notes)

## Basic usage

```cpp
QSpinBox *spin = new QSpinBox();
spin->setRange(0, 100);
spin->setSingleStep(10);
spin->setSuffix("%");
spin->setValue(10);

QObject::connect(spin, &QSpinBox::valueChanged, [](int value) {
	cout << "V=" << value << endl;
});

layout->addWidget(spin);
```

## Common operations

```cpp
spin->setMinimum(0);
spin->setMaximum(100);
spin->setPrefix("$");
spin->setSuffix("%");
spin->setWrapping(true);

int value = spin->value();
```

## Signals

* `valueChanged(int)` is emitted when the numeric value changes.
* `textChanged(QString)` is emitted when the displayed text changes, including prefix/suffix.

## Notes

* Use `QDoubleSpinBox` for floating-point values.
* `setWrapping(true)` allows moving from max back to min and from min back to max.

# QSlider

[← back](../qt-widgets.md)

`QSlider` lets the user choose an integer value from a range. It is useful for volume, zoom, brightness, progress-like settings, and other bounded values.

```cpp
#include <QSlider>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Tick marks](#tick-marks)
- [Signals](#signals)
- [Notes](#notes)

## <a id="basic-usage"></a>Basic usage

```cpp
QSlider *slider = new QSlider(Qt::Horizontal);
slider->setRange(0, 100);
slider->setValue(30);

QObject::connect(slider, &QSlider::valueChanged, [](int value) {
	cout << "S=" << value << endl;
});

layout->addWidget(slider);
```

## <a id="common-operations"></a>Common operations

```cpp
slider->setMinimum(0);
slider->setMaximum(100);
slider->setSingleStep(5);
slider->setPageStep(10);
slider->setValue(50);

int value = slider->value();
```

## <a id="tick-marks"></a>Tick marks

```cpp
slider->setTickPosition(QSlider::TicksAbove);
slider->setTickInterval(10);
```

## <a id="signals"></a>Signals

* `valueChanged(int)` is emitted when the value changes.
* `sliderMoved(int)` is emitted while the user drags the handle.
* `sliderReleased()` is useful when expensive work should run after dragging ends.

## <a id="notes"></a>Notes

* `setSingleStep()` affects keyboard movement.
* `setPageStep()` affects Page Up/Page Down and track clicks.
* Use `Qt::Vertical` for a vertical slider.

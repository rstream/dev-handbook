# QSlider

[← back](../qt-widgets.md)

Slider (horizontal/vertical)

```cpp
QSlider *slider = new QSlider(Qt::Horizontal);
slider->setRange(0, 100);
slider->setValue(30);
slider->setSingleStep(5); // keyboard!
slider->setPageStep(10); // pgup/pgdn + click to the left/right of the slider
slider->setTickPosition(QSlider::TicksAbove);
slider->setTickInterval(10);
QObject::connect(slider, &QSlider::valueChanged, [](int value) {
	cout << "S=" << value << endl;
});
layout->addWidget(slider);
```
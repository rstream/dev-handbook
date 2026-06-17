# Hello world application using Qt in C++

[← back](index.md)

This is a minimal Qt Widgets application. It creates a `QApplication`, opens a `QMainWindow`, adds a central widget with a layout, and shows a label.

## Summary

- [What this example shows](#what-this-example-shows)
- [Example](#example)
- [Notes](#notes)

## What this example shows

* `QApplication` owns the GUI event loop.
* `QMainWindow` is the top-level application window.
* `setCentralWidget()` defines the main content area.
* `QVBoxLayout` arranges child widgets vertically.

## Example

```cpp
#include <QApplication>
#include <QMainWindow>
#include <QLabel>
#include <QVBoxLayout>
#include <QWidget>

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    QMainWindow *win = new QMainWindow();
    QWidget *central = new QWidget();
    win->setCentralWidget(central);
    QVBoxLayout *layout = new QVBoxLayout(central);
    QLabel *label = new QLabel("Hello, world!");
    layout->addWidget(label);
    win->show();
    return app.exec();
}
```

## Notes

* A Qt Widgets app must create exactly one `QApplication` object.
* `app.exec()` starts the event loop and keeps the application running.
* Widgets added to a layout are managed through Qt parent ownership.

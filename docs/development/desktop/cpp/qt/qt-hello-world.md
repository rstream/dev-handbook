# Hello world application using Qt in C++

[← back](../index.md)

This is a sample "Hello World" application written using Qt in C++
* create a Main Window
* assign a widget to the Window
* create a layout for the widget
* add a label to the layout

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
# QTabWidget

[← back](../qt-widgets.md)

Multi-tab window

```cpp
QTabWidget *tabs = new QTabWidget();
//
QWidget *page1 = new QWidget();
QVBoxLayout *layout1 = new QVBoxLayout(page1);
QLabel *label1 = new QLabel("Content of the first tab!");
layout1->addWidget(label1);
//
QWidget *page2 = new QWidget();
QVBoxLayout *layout2 = new QVBoxLayout(page2);
QLabel *label2 = new QLabel("Content of the second tab!");
layout2->addWidget(label2);
//
tabs->addTab(page1, "First");
tabs->addTab(page2, "Second");
layout->addWidget(tabs);
```
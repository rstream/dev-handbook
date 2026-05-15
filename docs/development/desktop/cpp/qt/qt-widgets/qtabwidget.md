# QTabWidget

[← back](../qt-widgets.md)

`QTabWidget` shows several pages in the same area and lets the user switch between them using tabs.

```cpp
#include <QLabel>
#include <QTabWidget>
#include <QVBoxLayout>
#include <QWidget>
```

## Basic usage

```cpp
QTabWidget *tabs = new QTabWidget();

QWidget *page1 = new QWidget();
QVBoxLayout *layout1 = new QVBoxLayout(page1);
QLabel *label1 = new QLabel("Content of the first tab!");
layout1->addWidget(label1);

QWidget *page2 = new QWidget();
QVBoxLayout *layout2 = new QVBoxLayout(page2);
QLabel *label2 = new QLabel("Content of the second tab!");
layout2->addWidget(label2);

tabs->addTab(page1, "First");
tabs->addTab(page2, "Second");

layout->addWidget(tabs);
```

## Common operations

```cpp
tabs->setCurrentIndex(1);
int index = tabs->currentIndex();

tabs->setTabText(0, "General");
tabs->setTabEnabled(1, false);
tabs->removeTab(1);
```

## Closable tabs

```cpp
tabs->setTabsClosable(true);

QObject::connect(tabs, &QTabWidget::tabCloseRequested, [tabs](int index) {
    QWidget *page = tabs->widget(index);
    tabs->removeTab(index);
    delete page;
});
```

## Signals

* `currentChanged(int)` is emitted when the active tab changes.
* `tabCloseRequested(int)` is emitted when the user clicks a close button on a closable tab.

## Notes

* `addTab()` takes ownership of the page widget.
* Removing a tab does not automatically delete its page widget.

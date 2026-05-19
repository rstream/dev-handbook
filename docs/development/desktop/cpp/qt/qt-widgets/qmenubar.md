# QMenuBar, QMenu

[← back](../index.md)

`QMenuBar` adds an application menu to a main window. Menus contain `QAction` objects; the same action can also be reused in toolbars and context menus.

```cpp
#include <QAction>
#include <QKeySequence>
#include <QMenu>
#include <QMenuBar>
#include <QMessageBox>
#include <QStatusBar>
```

## Summary

- [Basic usage](#basic-usage)
- [Common operations](#common-operations)
- [Submenu](#submenu)
- [Signals](#signals)
- [Notes](#notes)

## <a id="basic-usage"></a>Basic usage

```cpp
QMenuBar *menu = win->menuBar();

QStatusBar *statusBar = win->statusBar();
statusBar->showMessage("Ready");

QMenu *menuTasks = menu->addMenu("Tasks");
QAction *actLog = new QAction("Log", win);
actLog->setStatusTip("Log something");
menuTasks->addAction(actLog);
menuTasks->addSeparator();

QAction *actExit = new QAction("Exit", win);
actExit->setStatusTip("Exit application");
menuTasks->addAction(actExit);

QMenu *menuHelp = menu->addMenu("Help");
QAction *actAbout = new QAction("About", win);
actAbout->setStatusTip("About this application");
menuHelp->addAction(actAbout);

QObject::connect(actLog, &QAction::triggered, []() {
	cout << "Menu : Log" << endl;
});

QObject::connect(actExit, &QAction::triggered, [&app]() {
	app.closeAllWindows();
});

QObject::connect(actAbout, &QAction::triggered, []() {
	QMessageBox::information(nullptr, "About", "This is a demo application");
});
```

## <a id="common-operations"></a>Common operations

```cpp
QAction *actSave = new QAction("Save", win);
actSave->setShortcut(QKeySequence::Save);
actSave->setStatusTip("Save current file");
menuTasks->addAction(actSave);

QAction *actToggle = new QAction("Show details", win);
actToggle->setCheckable(true);
actToggle->setChecked(true);
menuTasks->addAction(actToggle);
```

## <a id="submenu"></a>Submenu

```cpp
QMenu *recentMenu = menuTasks->addMenu("Recent files");
recentMenu->addAction("notes.txt");
recentMenu->addAction("report.txt");
```

## <a id="signals"></a>Signals

* `QAction::triggered()` is emitted when the action is activated.
* `QAction::toggled(bool)` is emitted for checkable actions.

## <a id="notes"></a>Notes

* `QMainWindow::menuBar()` creates or returns the window menu bar.
* `QAction` holds the menu item text, shortcut, status tip, checked state, and triggered signal.
* Status tips are shown in `QStatusBar` when the menu item is highlighted.

# QMenuBar, QMenu

[← back](../qt-widgets.md)

Menu (+ status bar)

```cpp
// get a window menu pointer
QMenuBar *menu = win->menuBar();

// enable status bar
QStatusBar *sb = win->statusBar();
sb->setStyleSheet("QStatusBar { border-top: 1px solid #aaa; border-left: 1px solid #aaa; border-bottom: 1px solid #fff; border-right: 1px solid #fff; margin: 1px; } ");

// menu item 1 - "Tasks"
QMenu *menuTasks = menu->addMenu("Tasks");
QAction *actLog = new QAction("Log"); actLog->setStatusTip("Log something");
menuTasks->addAction(actLog);
menuTasks->addSeparator();
QAction *actExit = new QAction("Exit"); actExit->setStatusTip("Exit application");
menuTasks->addAction(actExit);

// menu item 2 - "Help"
QMenu *menuHelp = menu->addMenu("Help");
QAction *actAbout = new QAction("About"); actAbout->setStatusTip("About this application");
menuHelp->addAction(actAbout);

// Actions
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
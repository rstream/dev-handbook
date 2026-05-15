# Simple dialogs using QMessageBox

[← back](index.md)

`QMessageBox` is used for simple modal dialogs: alerts, confirmations, warnings, errors, and "About" windows.

```cpp
#include <QMessageBox>
#include <QPushButton>
```

## Alert

Use `information()` for a simple notification.

```cpp
QMessageBox::information(
    win,
    "Saved",
    "Changes have been saved."
);
```

## Warning

Use `warning()` when the user should pay attention before continuing.

```cpp
QMessageBox::warning(
    win,
    "Invalid value",
    "Please enter a value from 1 to 100."
);
```

## Error

Use `critical()` for errors.

```cpp
QMessageBox::critical(
    win,
    "Save failed",
    "The file could not be saved."
);
```

## Confirmation

Use `question()` and check which button the user selected.

```cpp
QMessageBox::StandardButton answer = QMessageBox::question(
    win,
    "Delete item",
    "Delete the selected item?",
    QMessageBox::Yes | QMessageBox::No,
    // Default selected button.
    QMessageBox::No
);

if (answer == QMessageBox::Yes) {
    // delete item
}
```

## About dialog

Use `about()` for short application information.

```cpp
QMessageBox::about(
    win,
    "About",
    "Demo Qt application"
);
```

## Custom buttons

Create a `QMessageBox` instance when the dialog needs custom text for buttons.

```cpp
QMessageBox box(win);
box.setWindowTitle("Unsaved changes");
box.setText("Save changes before closing?");
box.setIcon(QMessageBox::Question);

// Keep the button pointer to check it after exec().
QPushButton *saveButton = box.addButton("Save", QMessageBox::AcceptRole);
box.addButton("Discard", QMessageBox::DestructiveRole);
box.addButton(QMessageBox::Cancel);

box.exec();

if (box.clickedButton() == saveButton) {
    // save changes
}
```

## Standard icons

Use these values with `setIcon()` when creating a `QMessageBox` instance.

| Icon | Meaning |
| --- | --- |
| `QMessageBox::NoIcon` | No icon |
| `QMessageBox::Information` | Informational message |
| `QMessageBox::Warning` | Warning or non-critical problem |
| `QMessageBox::Critical` | Error or critical problem |
| `QMessageBox::Question` | Question or confirmation |

```cpp
QMessageBox box(win);
box.setIcon(QMessageBox::Question);
```

## Standard buttons

Common standard buttons for message boxes.

| Button | Typical use |
| --- | --- |
| `QMessageBox::Ok` | Accept or close |
| `QMessageBox::Cancel` | Cancel action |
| `QMessageBox::Yes` | Confirm action |
| `QMessageBox::No` | Reject action |
| `QMessageBox::Save` | Save changes |
| `QMessageBox::Discard` | Discard changes |
| `QMessageBox::Close` | Close window/dialog |
| `QMessageBox::Retry` | Try operation again |
| `QMessageBox::Ignore` | Ignore problem and continue |
| `QMessageBox::Abort` | Stop operation |

```cpp
QMessageBox box(win);
box.setWindowTitle("Unsaved changes");
box.setText("Save changes before closing?");
box.setIcon(QMessageBox::Question);
box.setStandardButtons(
    QMessageBox::Save | QMessageBox::Discard | QMessageBox::Cancel
);
// Default selected button.
box.setDefaultButton(QMessageBox::Save);

QMessageBox::StandardButton answer =
    static_cast<QMessageBox::StandardButton>(box.exec());
```

## Button roles

Button roles are used with custom buttons. They describe what the button does.

| Role | Meaning |
| --- | --- |
| `QMessageBox::AcceptRole` | Accept the dialog |
| `QMessageBox::RejectRole` | Reject the dialog |
| `QMessageBox::DestructiveRole` | Perform a destructive action |
| `QMessageBox::ActionRole` | Perform an action without accepting/rejecting |
| `QMessageBox::HelpRole` | Open help |
| `QMessageBox::YesRole` | Yes-like answer |
| `QMessageBox::NoRole` | No-like answer |
| `QMessageBox::ApplyRole` | Apply changes |
| `QMessageBox::ResetRole` | Reset fields/settings |

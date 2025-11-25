# VS Code initial setup

[← back](index.md)

## 1. Disable Telemetry

**Navigate:**
> File > Preferences > Settings

Type **telemetry** to find telemetry-related options  
Set the following:  
* Feedback: Enabled = unchecked
* Telemetry Level = off

## 2. Set up local server extension — Live Preview

**Navigate:**
> View > Extensions  

Search for `Live Preview` and install it.  
For any HTML file, the preview button will appear in the **top-right corner**.

---

## 3. Install Darcula theme (WebStorm style)

Install extension `Webstorm Ui Theme For vscode`

**Then navigate to:**  
> File > Preferences > Theme > Color Theme

And choose your theme.

## 4. Set key bindings

Go to:  
> File > Preferences > Keyboard Shortcuts

**a)** Find `"saveAll"` — assign: `Ctrl+S`  
→ Saves **all opened files** (not only current).  
> 💡 *Note: You need to remove `Ctrl+S` from `"Save File"` first.*

**b)** Find `"Toggle block comment"` — assign: `Ctrl+Shift+/`  
→ *(WebStorm-like hotkey)*

**Linux Notes**
* editing key bindings as JSON: `F1` → `Preferences: Open Keyboard Shortcuts JSON`
* if `Ctrl+/` is not working for non-english keyboard layout (line comment) - bind it to `Ctrl+[Slash]` (using physical key instead - layout independent)
* if "Ctrl+Shift" is captured for keyboard layout switching, you can bind block comment to `Alt+Shift+[Slash]`

My key bindings:  
[for Windows](./assets/keybindings-windows.json)  
[for Linux](./assets/keybindings-linux.json)

## 5. Set default path

This sets the default path for **"Open File"** and **"Open Folder"** dialogs.

Go to:  
> File > Preferences > Settings > Text Editor > Files

Set the **"Default Path"** field to your desired folder.
# OpenSUSE - control display brightness

[← back](index.md)

## ddcutil

To set software adjustment of the display brightness on your desktop you need to install `ddcutil` and set up hotkeys.

### 1. Install ddcutil

```sh
sudo zypper install ddcutil
```

### 2. Enable I2C

Enable access to I2C devices
```sh
sudo modprobe i2c-dev
```

Check if I2C devices are present
```sh
ls /dev/i2c-*
```
The output should look like:  
`/dev/i2c-0  /dev/i2c-1  /dev/i2c-2  /dev/i2c-3  /dev/i2c-4  /dev/i2c-5  /dev/i2c-6`

### 3. Try ddcutil

#### Detect the display

Try if ddcutil detects the display:
```sh
ddcutil detect
```
You should see the detected display(s) settings
```
Display 1
   I2C bus:  /dev/i2c-2
   DRM connector:           card0-DP-1
   EDID synopsis:
      Mfg id:               HPN - UNK
      Model:                OMEN 27q
      Product code:         14660  (0x3944)
      Serial number:        CNC4191P88
      Binary serial number: 16843009 (0x01010101)
      Manufacture year:     2024,  Week: 19
   VCP version:         2.2
```

#### Work with brightness

Get current brightness level:
```sh
ddcutil getvcp 10
```

Set brightness to 25%:
```sh
ddcutil setvcp 10 25
```

Increase brightness (+10%)
```sh
ddcutil setvcp 10 + 10
```

Decrease brightness (-10%)
```sh
ddcutil setvcp 10 - 10
```

### 4. Make I2C load on startup

Navigate to `/etc/modules-load.d` and create a file `ddcutil.conf` with content:
```
# load i2c support for ddcutil
i2c-dev
```
You can use this command:
```sh
printf '# load i2c support for ddcutil\ni2c-dev' | sudo tee /etc/modules-load.d/ddcutil.conf
```

### 5. Create shortcuts

* Navigate to `START > Settings > System Settings > Shortcuts`
* Create a **Shortcut group**
* Create Global Shortcuts (command/URL) inside a Group:
  * Brightness Up: `/usr/bin/ddcutil setvcp 10 + 10`
  * Brightness Down: `/usr/bin/ddcutil setvcp 10 - 10`

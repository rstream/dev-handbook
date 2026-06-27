# OpenSUSE - troubleshooting

[← back](index.md)

## No audio device

Some Intel audio controllers are using SOF driver, and by default packages for it are not installed.

Install necessary packages:
```bash
sudo zypper install sof-firmware alsa-ucm-conf
```
* `sof-firmware` - the audio driver
* `alsa-ucm-conf` - configuration package, describes which speakers/plugs/etc exist for a specific audio adapter
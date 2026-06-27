# OpenSUSE - installation

[← back](index.md)

## Download and prepare media

You can download openSUSE ISO from the official site:  
https://get.opensuse.org/desktop/

Use **Rufus** (https://rufus.ie/) to write ISO file on the flash drive:
* Partition scheme = MBR
* Target system = BIOS or UEFI
* Other setting = default

## Installation

Boot from the installation disk and choose installation option (`Install Leap 16.0 (x86_674)`).  
Unlike v15.6 - you will get into the Agama installer (Firefox-based).

Choose regular installation (`Leap 16.0`) instead of micro (`openSUSE Leap Micro 6.2`).

The installation UI has several sections on the left side:
* Overview - overview of the current setup
* Hostname - change the name of the PC
* Localization - language, keyboard & time zone
* Network - set up network connection
* Storage - set up disk partitions
* Software - desktop selection and additional software
* Authentication

### Host name

Set the checkbox "Use static hostname" and create a name for your PC.

### Storage

Installer will suggest a default disk layout (EFI, Btrfs root, 2Gb swap).

To set up a custom disk layout:
* **Details**: click `New partitions will be created for "/" and "swap"`.
* Remove all existing planned partitions
* Create new partitions

> Note: due to the existing issue with the Agama installer you cannot create partitions with custom mount points during the installation (you can create only `/boot/efi`, `/`, `swap` and `/home`). Leave empty space and create those partitions later.

#### Disk layout

> Note: you don't have to create EFI partition - it would be created automatically once you create `/`.

Partitions setting:
* **EFI Boot Partition** (small boot partition)
    * file system: `FAT`
    * size: `500 Mb` (enough)
    * mount: `/boot/efi`
* **Operating System** (for the system)
    * file system: `Ext4`
    * size: `80 Gb`
    * mount: `/`
* **Swap** (special partition for Swap)
    * file system: `Swap`
    * size:
      * auto (recommended for most cases) - will make a 1-2 Gb swap
      * as RAM, like `16 Gb` (if using hybernation or running heavy RAM-consuming apps)
    * mount: `swap`

These partitions can be created only after the installation:

* **Data and ISV Applications** (fast partition for your work)
    * file system: `Ext4`
    * size: `128 Gb` (how much do you need for development?)
    * mount: `/data`
* **Data and ISV Applications** (big partition for media files and backups)
    * file system: `XFS`
    * size: `730 Gb` (the rest of space)
    * mount: `/stuff`

Notes:
* Don't mount any partition as `/home` - let's keep home directory on the system partition for easy system backups
* Ext4 is faster with small file - good for system and dev
* XFS is better with large files - choose it for media

#### Encryption

If this is a laptop for travels - it's a good idea to enable disk encryption. On modern laptops with hardware AES support it will not reduce the performance.

### Software

By default, no desktop is selected (you will get simple text-based UI).

To select a desktop:
* Click "Change selection"
* Choose a desktop, like "KDE Applications and Plasma Desktop" (some other items would be auto-selected)

### Authentication

#### First user

To create a user click **Define a user now** and enter username, login and password.

> Note: this user would be added to the `wheel` group: for all `sudo` operations you will have to enter this user's password (not root password).

#### Root user

Also, you can define a password for root user: click `edit` in the **Root user** section and define a password.

### Final steps

1. Check once again **Overview** section.
2. Click `Install` at the to-right corner.

## Post-install actions

### Create a partition for personal data

In openSUSE 16 you have to do it manually after the installation.

Use [Cockpit](suse-cockpit.md) to create new partition:

Enter Cockpit:
```
https://localhost:9090
```
* Navigate to the `Storage` section
* Select you disk drive
* Click three dots to the right of the `Free space` > `Create partition`
* Set file system type, size, mount point
* Enable encryption (`LUKS2` is recommended). set "Store passphrase" so the partition would be mounted at login without need to enter the passphrase

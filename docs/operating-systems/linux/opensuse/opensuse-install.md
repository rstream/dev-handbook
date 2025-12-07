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

Boot from the installation disk and choose `Installation`.

Activate `Online repositories`.

### Desktop selection

My favorite one is `KDE Plasma`.

### Disk partitioning

Select
> Expert Partitioner > Start with Existing Partitions

#### And set up partition manually

Partitions setting:
* **EFI Boot Partition** (small boot partition) 
  * file system: `FAT` 
  * size: `500 Mb` (enough)
  * mount: `/boot/efi`
* **Operating System** (for the system)
  * file system: `Ext4`
  * size: `64 Gb` (empty system needs 8-9 Gb, with soft - 12-16 Gb of space)
  * mount: `/`
* **Swap** (special partition for Swap)
  * file system: `Swap`
  * size: `8 Gb` (as RAM size - if using hybernation)
  * mount: `swap`
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

Click `Accept` and...

#### You will see the suggested layout

Layout configured manually using the Expert Partitioner.

Changes to partitioning:

• Create GPT on /dev/sda  
• Create partition /dev/sda1 (500.00 MiB) for /boot/efi with vfat  
• Create partition /dev/sda2 (64.00 GiB) for / with ext4  
• Create partition /dev/sda3 (8.00 GiB) for swap  
• Create partition /dev/sda4 (128.00 GiB) for /data with ext4  
• Create partition /dev/sda5 (730 GiB) for /stuff with xfs

Click `Next`

### Other steps

1. Select time zone
2. Create a user
3. Check the installation summary
4. Click `Install`
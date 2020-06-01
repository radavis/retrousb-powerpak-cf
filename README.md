# retrousb.com NES PowerPak CF Scripts

## `build`

Currently, this downloads unpacks all known mappers to the `build/POWERPAK` folder.

```bash
$ ./bin/build
```

Then, manually copy over your organized ROMS to the `build` folder.

## Format CF Card (macOS)

```bash
$ diskutil list
$ sudo diskutil eraseDisk FAT32 PWRPK_CF MBRFormat /dev/diskX
```

## Create PowerPak CF

[Copy files in alphabetical order](https://www.linuxquestions.org/questions/linux-general-1/copy-files-in-order-alphabetical-order-4175524438/#post5265624)

```bash
$ rsync -var ./build/* /Volumes/PWRPK_CF
```

## Backup CF Card

[Disk Cloning with DD](https://pbxbook.com/other/dd_clone.html)

```bash
$ diskutil list
$ diskutil unmountDisk /dev/diskX
$ sudo dd if=/dev/rdiskX of=img/512MB-CF-FAT32.img
$ cd img
$ zip 512MB-CF-FAT32.zip 512MB-CF-FAT32.img
$ rm 512MB-CF-FAT32.img
```

## Restore CF Card

```bash
$ unzip 512MB-CF-FAT32.zip
$ sudo dd if=512MB-CF-FAT32.img of=/dev/rdiskX
```

## PowerPak Specs

* Xilinx FPGA
* 512KB PRG space
* 32KB battery RAM space
* 512KB CHR space
* boot rom
* glue logic

## Resources

* [Product Homepage](https://www.retrousb.com/product_info.php?cPath=24&products_id=34)
  - [Mappers (POWERPAK134105.zip)](https://www.retrousb.com/downloads/POWERPAK134105.zip)
  - [Save File (8KBsave.zip)](https://www.retrousb.com/downloads/8KBsave.zip)
* [PowerPak (wiki.nesdev.com)](https://wiki.nesdev.com/w/index.php/PowerPak)
  - [Loopy's Mappers (powerpak_loopy.zip)](http://3dscapture.com/NES/powerpak_loopy.zip)
  - [PowerMappers (powermappers-v23.zip)](https://fo.aspekt.fi/downloads/powermappers-v23.zip)
  - [Myask's Mappers](http://forums.nesdev.com/download/file.php?id=5989)
* [NES Manuals](https://archive.org/details/NESManuals)
* [PowerMappers Compatibility Testing Spreadsheet](https://docs.google.com/spreadsheets/d/13s79Q6BdxXlUv3620TSkmeCReB94mvXkNxjyanKXXBw/edit#gid=1768544018)
* [List of NES games with a battery save](https://forums.nesdev.com/viewtopic.php?t=17181)

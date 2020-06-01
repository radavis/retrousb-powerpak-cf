# retrousb.com NES PowerPak CF Scripts

1. Add .SAV files to SAVES folder, named after Rom file
1. Get Top100 List

## Prepare `build` Folder

```bash
$ ./bin/clean
```

## Add Mappers

```bash
$ ./bin/retrousb-mappers
$ ./bin/loopy-mappers
$ ./bin/powermappers
$ ./bin/myask-mappers
```

## Download Roms

### archive.org [No-Intro ROM Sets](https://archive.org/details/no-intro-rom-sets)

```bash
$ mkdir "$(pwd)/temp/nointro"
$ wget https://archive.org/download/no-intro-rom-sets/Nintendo%20-%20Nintendo%20Entertainment%20System%20%2820200329-092100%29.zip \
    -O "$(pwd)/temp/nointro/nes.zip"
$ cd temp/nointro
$ unzip nes.zip
$ cd Nintendo\ -\ Nintendo\ Entertainment\ System
$ find . -type f | wc -l  # 3006

$ find . -name "*.zip" -exec unzip '{}' \;
$ rm *.zip

$ mkdir ../USA
$ find . -name "*USA*.nes" -exec mv '{}' ../USA \;

$ mkdir ../Japan
$ find . -name "*(Japan)*.nes" -exec mv '{}' ../Japan \;

...

$ cd ../USA
$ ./../../../bin/organize-roms
```

### archive.org [NES ROMS by EmuVault](https://archive.org/details/NESROMS)

```bash
$ aria2c --dir="$(pwd)/temp" https://archive.org/download/NESROMS/NESROMS_archive.torrent
$ cd temp/NESROMS
$ unzip NES_ROMS.zip
$ find . -type f | wc -l  # 3541 files
```

### archive.org [Cyles' NES Rom Pack](https://archive.org/details/CylesNESRomPack)

> [...] includes all current Translations as well as all current Hack titles.

Uploaded on 2019-03-15 05:15:22

```bash
$ aria2c --dir="$(pwd)/temp" \
    https://archive.org/download/CylesNESRomPack/CylesNESRomPack_archive.torrent
$ cd temp/CylesNESRomPack
$ unzip "Cyles' NES Rom Pack.zip"
$ find . -type f | wc -l  # 3003 files
```

## Copy Roms

```bash
$ cp -r temp/nointro/{Asia,Australia,Europe,Other,Spain,USA,World} ./build
```

## Format CF Card

```bash
$ sudo diskutil eraseDisk FAT32 PWRPK_CF MBRFormat /dev/disk3
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
$ diskutil unmountDisk /dev/disk3
$ sudo dd if=/dev/rdisk3 of=img/512MB-CF-FAT32.img
$ cd img
$ zip 512MB-CF-FAT32.zip 512MB-CF-FAT32.img
$ rm 512MB-CF-FAT32.img
```

## Determine if ROM uses NVRAM

```python
# https://forums.nesdev.com/viewtopic.php?t=17181#p215730

def needs_save(filename):
    if (filename.lower().endswith(".nes")):
        f = open(filename, "rb")
        f.seek(6)
        bb = ord(f.read(1))
        return ((bb & 0x02) != 0)
    return False
```

## Restore CF Card

```bash
$ unzip 512MB-CF-FAT32.zip
$ sudo dd if=512MB-CF-FAT32.img of=/dev/rdisk3
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
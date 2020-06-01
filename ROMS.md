## Roms

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

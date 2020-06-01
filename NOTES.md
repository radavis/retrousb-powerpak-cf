# Notes

* MMC5 is not fully implemented. This means Castlevania III and
  [other games using this mapper](https://wiki.nesdev.com/w/index.php/MMC5) will
  not work properly.

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

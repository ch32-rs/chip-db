# WCH32 Chip Database

Suggest, Use [Visual Studio Code](https://code.visualstudio.com) Edit the project

## Schema

```yaml
name: <string:CHxxx Series>
mcu_type: <u8>
device_type: <u8> # normally this is mcy_type + 0x10
support_usb: <bool>
support_serial: <bool>
support_net: <bool>
description: <string:Family description>
config_registers:
  # registers are parsed in LE mode
  - offset: <u8:0x00, offset in the 12-byte config reply>
    name: <string:NAME_OF_REGISTER>
    description: <string>
    reset: <u32:0x00FF5AA5> # a u32 value, used to reset chip config, like unprotect
    fields:
      - bit_range: [7, 0] # inclusive range, [MSB, LSB]
        name: <string:NAME_OF_FIELD>
        description: <string>
        explaination:
          0xa5: Unprotected # an explaination to field value
          _: Protected # matches all remaining cases
variants:
  - name: <string:CHXXX, unique id of the chip, with or without variant surfix>
    chip_id: 0x30
    alt_chip_ids: ["ALL"] # special fix to probe all chip variants
    flash_size: 64K # 0x10000, 64KiB, 64KB, 64K
    eeprom_size: 32K
    eeprom_start_addr: 0x0
    support_usb: true # config can overwrite faimily config
    support_serial: true
    support_net: false
```

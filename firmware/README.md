# Firmware

To reflash the badge to it's original state, you'll need [esptool.py](https://github.com/espressif/esptool)

One you have it, run:
`esptool.py --chip esp32 --port "<YOUR_PORT>" --baud 921600 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 40m --flash_size detect 0x1000 bootloader_dio_40m.bin 0x8000 partitions.bin 0xe000 boot_app0.bin 0x10000 TC0xA.bin`

## Firmware Descriptions

#### TC0xA.bin
This is the provided "original firmware" from https://github.com/poplicola/Thotcon0xA_Pub

This firmware contains embedded WAV files, and connects to an irc server at irl.depaul.edu.  It checks http://rudy.io/TC0xA.bin for an update

#### TC0xA.bin.rudy.io
This is the firmware update from http://rudy.io/TC0xA.bin that the "original" firmware updates itself with.  It connects to 10.0.38.202, but other than that not sure how it forces an update using irl.depaul.edu

#### TC0xA.bin.irl.depaul.edu
This is the firmware update from http://irl.depaul.edu/TC0xA.bin

- changing the update server to http://irl.depaul.edu/TC0xA.bin
- removing all of the !play* IRC commands


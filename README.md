# THOTCON 0xA Badge Hijacking #

The Thotcon 0xA badge runs an ESP32 chip; the stock badge firmware process is:

- connect to the THOTCON-Static WPA2-PSK secured SSID, with password thotcon0xa
- check for an update at http://irl.depaul.edu/TC0xA.bin, apply if it exists and is a new version
- connect to an IRC command and control server at irc://irl.depaul.edu:6969/#c2c
- execute any commands in the topic of the channel, or that are posted in the channel.

This project hijacks this process, creating an evil twin access point and running our own IRC and HTTP servers to capture and control and badge we can force to connect to us.

### Completed ###
- Evil Twin Access Point
- IRC server
- HTTP Server

### Uncompleted (time contraints) ###
- Limiting client types to be badges only
- New firmware that contains new update or IRC CnC urls
- Deauthing badges that are connected to other BSSIDs

## Running the project ##
It is expected you are running this on Kali Linux 2019.1; adjust accordingly.  Either run each command in a new terminal or background the processes

- `apt install hostapd dnsmasq irssi`
- `hostapd hostapd.conf`
- `ifconfig wlan0 up 192.168.55.1 netmask 255.255.255.0`
- `route add -net 192.168.55.0 netmask 255.255.255.0 gw 192.168.55.1`
- `dnsmasq -C dnsmasq.conf -d`
- `ngircd -f ngircd.conf -n`
- `sudo python server.py`
- `irssi -c irl.depaul.edu`

## Firmware Versions ##
- original_firmware.bin => first firmware dump from the badge


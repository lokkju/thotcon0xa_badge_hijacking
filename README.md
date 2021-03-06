# THOTCON 0xA Badge Hijacking #

The Thotcon 0xA badge runs an ESP32 chip; the final badge firmware process is:

- connect to the THOTCON-Static WPA2-PSK secured SSID, with password thotcon0xa
- check for an update at http://irl.depaul.edu/TC0xA.bin, apply if it exists and is a new version
- connect to an IRC command and control server at irc://irl.depaul.edu:6969/#c2c
- execute any commands in the topic of the channel, or that are posted in the channel.

This project hijacks this process, creating an evil twin access point and running our own IRC and HTTP servers to capture and control any badge we can force to connect to us.

Over the course of the conference, I was able to capture at least 40 badges - and that was without even deauthing.

### Completed ###
- Evil Twin Access Point
- IRC server
- HTTP Server

### Uncompleted (time contraints) ###
- Limiting client types to be badges only
- New firmware that contains new update or IRC CnC urls
- Deauthing badges that are connected to other BSSIDs
- New firmware that spreads itself, as the ESP32 can emulated an AP itself.

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

### Forcing your own firmware to be loaded
To force your own firmware to be loaded, you'll have to either generate new firmware (not suggested) or edit an existing firmware (see the firmware directory); then just put that edited firmware as TC0xA.bin in this directory, and the python script will serve it.

Hardware Used:
1) Raspberry Pi Zero v1.3
2) Long Range Wireless Adapter w/ 5dBi Antenna - 8192CUS Chipset - Plug and play! (https://www.amazon.com/gp/product/B00YI0AIRS)
3) Tiny OTG Adapter Micro USB to USB - (https://www.adafruit.com/product/2910)
4) Micro SD card

Handy how-to's:
https://www.raspberrypi.org/documentation/installation/installing-images/linux.md
https://www.raspberrypi.org/forums/viewtopic.php?t=191252


Below is a personal reference for commands I used on my linux system.
Please follow the how-to links,  as some of the below could do bad things if you do it to the wrong device.
For example, you could easily overwrite your hard drive if you get the device name wrong.

From a linux machine:

get latest image
$ wget https://downloads.raspberrypi.org/raspbian_lite_latest

plug in sd card and locate it
$ lsblk  

Example card located at /dev/sdb
unmount any partitions on your sd card if they exist
$ umount /dev/sdb1

unzip and write image to sd card - assumes 2018-06-27 version of stretch and device at /dev/sdb
$ unzip -p 2018-06-27-raspbian-stretch.zip | sudo dd of=/dev/sdb bs=4M conv=fsync

unplug and re insert sd card to mount to filesystem
navigate to boot directory of image
ssh disabled by default. to enable, create empty ssh file in boot directory
$ touch ssh

setup wireless by creating wpa_supplicant.conf in boot directory
$ vi wpa_supplicant.conf

country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="your_real_wifi_ssid"
    scan_ssid=1
    psk="your_real_password"
    key_mgmt=WPA-PSK
}

image is now ready for pi to boot headless and be logged into remotely via ssh
insert sd card and boot pi
use router admin portal to find ip address of pi

$ ssh pi@192.168.X.X

yay! logged into pi
expand filesystem, etc.
$ sudo raspi-config

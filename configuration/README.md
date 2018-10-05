Hardware Used:
1) Raspberry Pi Zero v1.3
2) Long Range Wireless Adapter w/ 5dBi Antenna - 8192CUS Chipset - Plug and play!<br /> (https://www.amazon.com/gp/product/B00YI0AIRS)
3) Tiny OTG Adapter Micro USB to USB<br /> (https://www.adafruit.com/product/2910)
4) Micro SD card

Handy how-to's:<br />
https://www.raspberrypi.org/documentation/installation/installing-images/linux.md 
https://www.raspberrypi.org/forums/viewtopic.php?t=191252


Below is a personal reference for commands I used on my linux system.
Please follow the how-to links,  as some of the below could do bad things if you do it to the wrong device.
For example, you could easily overwrite your hard drive if you get the device name wrong.

From a linux machine:

Get latest image<br />
$ wget https://downloads.raspberrypi.org/raspbian_lite_latest

Plug in sd card and locate it<br />
$ lsblk  

Example card located at /dev/sdb <br />
Unmount any partitions on your sd card if they exist <br />
$ umount /dev/sdb1

Unzip and write image to sd card - assumes 2018-06-27 version of stretch and device at /dev/sdb <br />
$ unzip -p 2018-06-27-raspbian-stretch.zip | sudo dd of=/dev/sdb bs=4M conv=fsync

Unplug and re insert sd card to mount to filesystem <br />
Navigate to boot directory of image <br />
SSH disabled by default. To enable, create empty ssh file in boot directory <br />
$ touch ssh

Setup wireless by creating wpa_supplicant.conf in boot directory <br />
$ vi wpa_supplicant.conf

<em>country=US  <br />
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev  <br />
update_config=1  <br />

network={ <br />
    ssid="your_real_wifi_ssid" <br />
    scan_ssid=1 <br />
    psk="your_real_password" <br />
    key_mgmt=WPA-PSK <br />
} <br /></em>

Image is now ready for pi to boot headless and be logged into remotely via ssh <br />
Insert sd card and boot pi <br />
Use router admin portal to find ip address of pi <br />

$ ssh pi<i></i>@192.168.X.X

Yay! Logged into pi. Expand filesystem, etc. <br />
$ sudo raspi-config

# Image Creation and Flashing


Link to the current arm64 OS: https://downloads.raspberrypi.org/raspios_arm64/images/

## Booting from USB
- Flash raspios Lite
- add `ssh` to boot dir
- update the system including the bootloader:
```sh
sudo apt update
sudo apt full-upgrade
sudo reboot
```
- use raspi-config to choose between SD/USB (default) or SD/Network boot modes.


## Create image

### On RPI
You can create an image and put it on an USB stick if you do not have Linux PC.
However, we advise to follow the instructions below when you have a Linux PC.

To check the partitions are what you are expecting:
```lsblk```

Create the directory for mounting:
```
sudo mkdir /media/usb
sudo chmod 775 /media/usb
```

Mount the USB connected device.  A single partition Fat32 USB stick on sdb1 in this case:
```
sudo mount -t exfat /dev/sda1 /media/usb -o rw,umask=0000
```

Make an img file from the card inserted in the Pi microSD card slot. Will take some time:
```
sudo dd if=/dev/mmcblk0 of=/media/usb/midas.img conv=fsync bs=4M status=progress
```

Shrink the image with PiShrink
```
wget https://raw.githubusercontent.com/Drewsif/PiShrink/master/pishrink.sh
chmod +x pishrink.sh

sudo pishrink.sh -z /media/usb/midas.img
```

Your image is now zipped and available on the USB stick to be flashed.


### On a Linux computer
Insert the SD-card of your RPI in your computer and copy the contents.

```
sudo dd if=/path/to/sdcard of=/path/to/midas.img conv=fsync bs=4M status=progress
```

Shrink the image with PiShrink
```
wget https://raw.githubusercontent.com/Drewsif/PiShrink/master/pishrink.sh
chmod +x pishrink.sh

sudo pishrink.sh -z /path/to/midas.img
```

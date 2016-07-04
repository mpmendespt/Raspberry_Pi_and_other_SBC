---
layout: post
title: Install Arch Linux on Raspberry Pi
category: ArchLinux Arch Linux Raspberry Pi
---

Currently neither [Raspberry Pi](https://www.raspberrypi.org/) nor the
[Arch Linux ARM](http://archlinuxarm.org/) website offer an image ready
for use of Arch Linux for Raspberry Pi. So i followed this steps on
Linux (in my case another Raspberry with a USB Pen Drive):

1.  Download the image for Raspberry Pi (ARM).

    ```ruby
	wget http://archlinuxarm.org/os/ArchLinuxARM-rpi-2-latest.tar.gz
	```

2.  Create a image file of 2GB:

    ```ruby
	dd if=/dev/zero of=arch.img bs=1M count=1850

    count=1850   
    1850+0 records in   
    1850+0 records out   
    1939865600 bytes (1.9 GB, 1.8 GiB) copied, 53.2323 s, 36.4 MB/s
	```

3.  [Partition the image file]:

    ```ruby
	fdisk arch.img
	```

    1.  Type **o**. This will clear out any partitions on the drive.
    2.  Type **p** to list partitions. There should be
        no partitions left.
    3.  Type **n**, then **p** for primary, **1** for the first
        partition on the drive, press ENTER to accept the default first
        sector, then type **+100M** for the last sector.
    4.  Type **t**, then **c** to set the first partition to type W95
        FAT32 (LBA).
    5.  Type **n**, then **p** for primary, **2** for the second
        partition on the drive, and then press ENTER twice to accept the
        default first and last sector.
    6.  Write the partition table and exit by typing **w**.

4.  Check the partitions created:

    ```ruby
	fdisk -l arch.img    
	
    Device Boot Start End Sectors Size Id Type   
    arch.img1 2048 206847 204800 100M c W95 FAT32 (LBA)    
    arch.img2 206848 3788799 3581952 1.7G 83 Linux
	```

5.  Mount the **boot** partition [^1]:

    ```ruby
	sudo losetup -v -f -o $((2048 * 512)) --sizelimit 104857600
    arch.img
	```

6.  Mount the **root** partition:

    ```ruby
	sudo losetup -v -f -o $((206848 * 512)) --sizelimit 1833959424
    arch.img

    sudo fdisk -l /dev/loop0

    Disk /dev/loop0: 100 MiB, 104857600 bytes, 204800 sectors    

    sudo fdisk -l /dev/loop1    

    Disk /dev/loop1: 1.7 GiB, 1833959424 bytes, 3581952 sectors
	```

7.  Format and mount **boot** partition

    ```ruby
	sudo mkfs.vfat /dev/loop0

    mkdir boot

    sudo mount /dev/loop0 boot
	```

8.  Format and mount **root** partition

    ```ruby
	sudo mkfs.ext4 /dev/loop1

    mkdir root

    sudo mount /dev/loop1 root
	```


9.  Extract **image** files:

    ```ruby
	sudo bsdtar -xpf ArchLinuxARM-rpi-2-latest.tar.gz -C root

    sync
	```

10. Copy **boot** files:

    ```ruby   
	sudo mv root/boot/* boot   

    sync   
	```

11. Unmount partitions:

    ```ruby
	sudo umount boot root

    rmdir boot root
	```

12. Detach partitions:

    ```ruby
	sudo losetup -d /dev/loop0

    sudo losetup -d /dev/loop1
	```

The image is ready!!

Now I copy it to my windows:

```ruby
"C:\Program Files (x86)"\PuTTY\pscp pi@192.168.1.110:/mnt/usbdrive/archlinux/arch.img "C:\tmp"
```

Then we can write it on SD card with
[Win32DiskImager](https://sourceforge.net/projects/win32diskimager/)
utility.    

![](/images/Win32DiskImager.png)


Insert the SD card into the Raspberry Pi, connect ethernet, and apply 5V
power.

-   Login as the default user ***alarm*** with the password ***alarm***.
-   The default root password is ***root***.

### References 

- <http://blog.schertel.co/posts/2015/08/arch-linux-arm-image-for-raspberry-pi/>   
- <http://elinux.org/ArchLinux_Install_Guide>   

[Partition the image file]: https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3
   
[^1]: <https://unix.stackexchange.com/questions/72443/cannot-mount-img-file-not-a-directory-error/72449#72449>   


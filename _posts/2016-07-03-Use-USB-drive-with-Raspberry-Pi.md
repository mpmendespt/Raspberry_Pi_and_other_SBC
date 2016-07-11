---
layout: post
title: Use USB hard disk & flash drives with Raspberry Pi
category: USB drive Raspberry partition Format Mount
---

Here we have a summary of the commands on how to mount a USB drive on
Raspberry.

Connecting and Mounting a USB Drive
-----------------------------------

After inserting a USB drive you will need to manually mount the device
in order to use it as additional USB storage for Raspberry Pi.

To reveal the correct name for the USB device:

```ruby
sudo ls /dev/sd*
/dev/sda  /dev/sda1
```


*If there is no partitions on device the result can be:*


```ruby
/dev/sda
```

### Create a partition on the divice:


```ruby
sudo fdisk /dev/sda


Command (m for help): p

Disk /dev/sda: 29.6 GiB, 31750881280 bytes, 62013440 sectors

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0xe85e0063

Command (m for help): n

Partition type

 p primary (0 primary, 0 extended, 4 free)

 e extended (container for logical partitions)

Select (default p): p

Partition number (1-4, default 1):

First sector (2048-62013439, default 2048):

Last sector, +sectors or +size{K,M,G,T,P} (2048-62013439, default
62013439):

Created a new partition 1 of type 'Linux' and of size 29.6 GiB.

Command (m for help): p

Disk /dev/sda: 29.6 GiB, 31750881280 bytes, 62013440 sectors

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0xe85e0063

Device Boot Start End Sectors Size Id Type

/dev/sda1 2048 62013439 62011392 29.6G 83 Linux

Command (m for help): w

The partition table has been altered.

Calling ioctl() to re-read partition table.

Syncing disks.
```

**Now, fdisk -l, will show the created partition**

```ruby
sudo fdisk -l

Device Boot Start End Sectors Size Id Type

/dev/sda1 2048 62013439 62011392 29.6G 83 Linux
```

### To list your file systems:

*sudo fdisk -l   
sudo mount -l   
df -h*   

### Format a drive to EXT4

*sudo mkfs.ext4 /dev/sda1 -L untitled*

### Add Apple OS X HFS+ read/write support

*sudo apt-get install hfsutils hfsprogs hfsutils*

### Format a drive to HFS+

*sudo mkfs.hfsplus /dev/sda1 -v untitled*

### Add Windows NTFS read/write support

*sudo apt-get install ntfs-3g*

### Format a drive to NTFS

*sudo mkfs.ntfs /dev/sda1 -f -v -I -L untitled*

### Add Windows/DOS FAT32 read/write support

*sudo apt-get install dosfstools*

### Format a drive to FAT32

*sudo mkfs.vfat /dev/sda1 -n untitled*



### We choose EXT4, so Format a drive to EXT4:

```ruby
sudo mkfs.ext4 /dev/sda1 -L untitled



mke2fs 1.42.12 (29-Aug-2014)

Creating filesystem with 7751424 4k blocks and 1941504 inodes

Filesystem UUID: 1dc1e005-05d8-42c1-a7a0-325c204f67a9

Superblock backups stored on blocks:

 32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 4096000



Allocating group tables: done

Writing inode tables: done

Creating journal (32768 blocks): done

Writing superblocks and filesystem accounting information: done
```


## To mount a USB drive:

Create the mount point:

```ruby
sudo mkdir /mnt/usbdrive
```

### Now connect the device to its mount point:

```ruby
sudo mount /dev/sda1 /mnt/usbdrive\
ls /mnt/usbdrive
```


```ruby
df -h

Filesystem      Size  Used Avail Use% Mounted on

/dev/root        15G  1.4G   13G  11% /
devtmpfs        459M     0  459M   0% /dev
tmpfs           463M     0  463M   0% /dev/shm
tmpfs           463M   18M  446M   4% /run
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           463M     0  463M   0% /sys/fs/cgroup
/dev/mmcblk0p1   63M   21M   43M  33% /boot
/dev/sda1        29G   44M   28G   1% /mnt/usbdrive
```


### Now we need to make sure the Pi user owns this folder:    

```ruby
sudo chown -R pi:pi /mnt/usbdrive
```


### Test:

```ruby
touch /mnt/usbdrive/test1
ls -l /mnt/usbdrive
total 16
drwx------ 2 pi pi 16384 Jul  3 14:52 lost+found
-rw-r--r-- 1 pi pi     0 Jul  3 15:00 test1
```

### Before disconnecting a USB drive:

```ruby
sudo umount /dev/sda1
```


*You don’t need to manually un-mount if you shutdown your Pi but if you
need to remove the drive at any other time you should un-mount it first.*



### Auto Mount


If we want the USB drive to be mounted when the system starts we can
edit the fstab file:

```ruby
sudo nano /etc/fstab
```

Then add the following line at the end :

**/dev/sda1 /mnt/usbdrive ext4 defaults,noatime 0 1**



```ruby
#/etc/fstab
proc /proc proc defaults 0 0
/dev/mmcblk0p1 /boot vfat defaults 0 2
/dev/mmcblk0p2 / ext4 defaults,noatime 0 1
# a swapfile is not a swap partition, no line here
# use dphys-swapfile swap\[on|off\] for that
/dev/sda1 /mnt/usbdrive ext4 defaults,noatime 0 1
```

The drive will mount at boot if it is attached to the Pi. If you want to mount the drive after you have plugged it in, use mount with the -a option.
Which mean: Mount  all  filesystems  (of the given types) mentioned in fstab.

```ruby
sudo mount -a
```


### References:

- <https://devtidbits.com/2013/03/21/using-usb-external-hard-disk-flash-drives-with-to-your-raspberry-pi/>   
- <http://www.makeuseof.com/tag/how-to-add-usb-storage-to-the-raspberry-pi/>   
- <http://www.raspberrypi-spy.co.uk/2014/05/how-to-mount-a-usb-flash-disk-on-the-raspberry-pi/>   
- <https://thepihut.com/blogs/raspberry-pi-tutorials/17699796-formatting-and-mounting-a-usb-drive-from-a-terminal-window>      
- <https://vicpimakers.ca/tutorials/raspberry-pi/usb-hard-disk-or-flash-drive-with-raspberry-pi/>   
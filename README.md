# raspberry-quick-setup

## Download an image (OS)

Visit [raspberrypi downloads](https://www.raspberrypi.org/downloads/)

## Create the SD card

cd to the directory the .zip file was downloaded

**unzip** the file

```
$ unzip your-image.zip
```

**find your device**

```
$ sudo fdisk -l
```
Usually the /dev/sda* partitions are your system's but not always.
**Warning** Be completely sure that you can identify your sd card otherwise you
will damage your system's partitions in the following step.
A safe way to find it is to run the fdisk command before inserting the sd card
and one more time after inserting it, then compare the outputs.

**disk cloning**

```
$ sudo dd bs=4M if=your-image.iso of=/dev/your-device conv=fsync status=progress
```

## Enable ssh

Mount the boot partition, run once again **fdisk -l**. The boot partition will
be the smaller of the two.

```
$ sudo mount /dev/boot-partition /mnt/
```

Create the ssh file

```
$ sudo touch /mnt/ssh
```

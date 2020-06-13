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
## Expand Filesystem

```
$ sudo raspi-config
```
Advanced Options > Expand Filesystem


## Add new user

```
$ useradd -m username
$ passwd username
```

## Add new user to sudo group

```
$ sudo visudo
```

Append it with:

```
username ALL=(ALL:ALL) ALL
```
## Delete default user (pi)

```
$ sudo userdel -r pi
```

## Setup SSH keys

SSH to Raspberry Pi without typing your password every time

#### Generate SSH keys

If you do not already have a private and public key, proceed

```
$ ssh-keygen
```

#### Copy the public key to Raspberry Pi

There are two methods

1.
```
$ cat ~/.ssh/id_rsa.pub | ssh <USERNAME>@<IP-ADDRESS> 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
```

2.
```
$ ssh-copy-id <USERNAME>@<IP-ADDRESS>
```

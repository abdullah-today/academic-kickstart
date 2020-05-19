---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Efistub"
subtitle: ""
summary: ""
authors: []
tags: ['efistub', 'efi', 'bootloaders', 'grub']
categories: []
date: 2019-05-19T14:55:37+05:00
lastmod: 2019-05-19T14:55:37+05:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: "EFISTUB"
  focal_point: "Smart"
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---


So in this post I'm gonna guide you how you can use efistub, a feature which you can use to boot the kernel without an extra boot manager(grub, systemd-boot, rEFInd etc.)
            
Create a boot entry using efibootmgr.

```sh
# efibootmgr --create --disk /dev/sda --part 1 --label Debian --loader /vmlinuz --unicode "root=/dev/sda2 rw initrd=\initrd.img" --verbose
```
    
Explaination of the command.

```sh
 --create 'creates a new boot entry'
 --disk   'disk where you wanna create the boot entry'
 --part   'partition number'
 --label  'the label for new entry'
 --loader 'loader to boot, it's vmlinuz in this example'
 --unicode 'kernel parameters you can define here like initrd, swap, encrypted container for root'
 --verbose 'let it verbose'
```

I have an encrypted installation on my machine so here is how I create an entry for me.
   
```sh
# efibootmgr --create --disk /dev/sda --part 1 --label 'My Debian' --loader /vmlinuz --unicode "cryptdevice=UUID=XXXXXXXXXXXXXXXXXX:cryptlvm root=UUID=XXXXXXXXXXXXXXXXXX rw initrd=\initrd.img resume=UUID=XXXXXXXXXXXXXXXXX" --verbose
```

where cryptdevice UUID is the UUID of my SSD's encrypted container's UUID and root's UUID is the UUID for my lvm volume where root is located, resume UUID is the lvm UUID where swap partition is. You can get UUID with blkid command. 


Now go to /boot directory and check for the vmlinuz and initrd.img. They might be in child directories like if EFI/grub or maybe somewhere else depending on your current boot managers. and move them to /boot. Also change your fstab (/etc/fstab) so that it mount your boot partition on /boot.

```sh
# mv /boot/efi/grub/vmlinuz-4.19.0-1-rt-amd64 /boot/vmlinuz
# mv /boot/efi/grub/initrd.img-4.9.0-8-amd64 /boot/initrd.img
```
and your fstab should be look like this.

```sh
UUID=XXXX-XXXX    /boot     vfat    umask=0077  0   1
```

By default, debian installs kernel and initrd images with their version numbers. But also puts a symlink to it in / with vmlinuz name. So we have to write a script so that if we get an update of kernel, it will automatically rename it to vmlinuz and initrd.img. Just create a script with following path and make it executable. 

```sh
# vim /etc/kernel/postinst.d/update-efistub

#!/bin/sh
cp /vmlinuz /boot/

```
save it and make it executable.

```sh
# chmod +x /etc/kernel/postinst.d/update-efistub
```


and do the same with initramfs.

```sh
# vim /etc/initramfs/post-update.d/update-efistub

#!/bin/sh
cp /initrd.img /boot/

```

make it executable.

```sh
chmod +x /etc/initramfs/post-update.d/update-efistub
```

That's it. Now uninstall any extra boot manager and reboot. You'll see that your machine is booting without a boot manager. Yeah, you heard it right. No sensible person will call it bootloader. They are just boot managers which also create an entry just like we did. So why don't we do it ourselves. Feel free to mail me if you get some errors.

> **_NOTE:_** On a standard debian installation, installer creates an *ESP* if
not already exists, and formats it as vFAT. And also creates another ext2
formatted partition. Installer mounts *ESP* as */boot/efi*. So for debian
standard install, your command looks like this.
```sh
# efibootmgr --create --disk /dev/sda --part 1 --label Debian --loader
'\EFI\debian\vmlinuz' --unicode 'root=UUID=XXXX-XXXX-XXXX-XXX ro quiet
initrd=\\EFI\\debian\\initrd.img' --verbose
```

and for an encrypted installation with lvm, it should be.

```sh
# efibootmgr --create --disk /dev/sda --part 1 --label Debian --loader
'\EFI\debian\vmlinuz' --unicode 'cryptdevice=UUID=XXXX-XXXX-XXXX-XXXX:cryptlvm
root=UUID=XXXX-XXXX-XXXX-XXXX ro quiet initrd=\\EFI\\debian\\initrd.img
resume=UUID=XXXX-XXXX-XXXX-XXXX' --verbose
```
where first UUID is your /dev/sda3 encrypted container UUID, root UUID is where
rootfs is installed and resume UUID is your encrypted swap partition UUID.




### Did you find this page helpful? Consider sharing it 🙌

---
date: '2024-12-07T11:57:56+07:00'
draft: false
title: 'How To Get Out of Linux Emergency Fucking Mode'
autonumber: true
toc: false
hideBackToTop: false
tags: ["rant", 'tutorial']
---
``` this is me ranting, nothing new nor useful here```
## Never Hard Shutdown
So recently i had this problem because of hard shutdown, when i use [TimeShift](https://github.com/linuxmint/timeshift), it freezes (should've use [Snapper](https://wiki.archlinux.org/title/Snapper) anyway) and i panically turn off my laptop. I boot and kazoot it went to emergency mode, i cant even login to root (because it's disabled by default on Fedora)
> LESSON LEARNED: never hard shutdown when messing with system files

## Solution
Enough yapping, here's the solution  
1. Follow [this](https://docs.fedoraproject.org/en-US/quick-docs/grub2-bootloader/#_restoring_the_bootloader_using_the_live_disk) (also [this](https://docs.fedoraproject.org/en-US/quick-docs/root-account-locked/) if you want to enable root account). When it comes to mounting the root partition, instead of doing this:
```
mount /dev/sda3 /mnt -o subvol=root
```
change it to:
```
mount /dev/sda3 /mnt -o subvol=@
```
this only applies if you use [TimeShift](https://github.com/linuxmint/timeshift) with btrfs because for some reason the root has to be @ instead of /
> NOTE: change /dev/sda3 to your disk partition, mine happen to be /dev/nvme0n1p6

2. Reinstall the grub stuff
```
dnf reinstall shim-\* grub2-efi-\* grub2-common
grub2-mkconfig -o /boot/grub2/grub.cfg
sync && exit
```
but wait, i've tried all this and my system still wont boot?  
well here comes the motherfucker that fucks it all, IT'S THE KERNEL!  
when i run ```systemctl --failed``` it says failed to mount boot-efi, although i've mount it correctly (maybe i didn't mount it correctly? but i can never be wrong). So if this problem occurs try reinstalling linux kernel ```dnf reinstall kernel*``` or use your old kernel (if it still exists)

## Conclusion
Love and Hate is not mutually exclusive.

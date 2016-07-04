# H. Aftian

A utility to create a BlankOn UEFI bootable USB.

## Steps

0. Get haftian
1. Prepare your BlankOn .ISO
2. Prepare your USB disk (this will be handled later) as GPT with 1 partition, formatted with FAT32 and mount it to somewhere
3. Run haftian:

```
cd /where/you/put/haftian/
sudo ./haftian /where/is/your.iso.file /where/you/mount/your/usb.disk
```

4. Reboot and try

# LICENSE

haftian is in public domain but it contains files from GRUB which are licensed in GPL3.


# Tips

This is how I prepare my USB disk. Note that `#` is Linux prompt and `(parted)` is GNU Parted prompt.

```
# sudo parted /dev/your/usb/device

(parted) mktable gpt
(parted) mkpart efi fat32 1 -1
(parted) toggle 1 boot
(parted) p 
Model: SanDisk Ultra (scsi)
Disk /dev/sdb: 8004MB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End     Size    File system  Name  Flags
 1      1049kB  8004MB  8003MB  fat32        efi   boot, esp
(parted) quit
# sudo mkfs.vfat -F32 /dev/your/usbdevice1    # <---- Don't forget to put partition number, if your usb disk is in /dev/sdb then this should be mkfs.vfat -F32 /dev/sdb1
# sudo mount /dev/your/usbdevice1 /mnt
```

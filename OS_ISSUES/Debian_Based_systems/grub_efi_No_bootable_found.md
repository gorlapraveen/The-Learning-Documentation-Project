

**Issues Related:** `The 'grub-efi-amd64-signed' package failed to install target/ [duplicate]` , `No Bootable device founs, insert bootable device found` , `error: /dev/sda1/ I/O error`

**Tags**: `ubuntu`, `debian`

-----------------------------------------

Try this if it makes sense to you:

1. Boot Ubuntu Live DVD/USB in testing mode and open terminal

2. Run installation process without installing boot loader by:

        sudo ubiquity -b

3. Press Continue testing after installation is over.

4. Mount the newly installed file system into /mnt:

        sudo mount /dev/sda2 /mnt

        sudo mkdir /mnt/boot/efi

        sudo mount /dev/sda1 /mnt/boot/efi

        for i in /dev /dev/pts /proc /sys; do sudo mount -B $i /mnt$i; done

(Where `sda2` is the root partition and sda1 is the EFI partition.)

5. Load the `efivars` module by:

         sudo modprobe efivars

6. Reinstall `grub-install` for a 64-bit version:

        sudo apt-get install --reinstall grub-efi-amd64-signed
        
        sudo grub-install --no-nvram --root-directory=/mnt

7. Change root to /mnt and update Grub:

        sudo chroot /mnt

        update-grub

8. Move and rename the installed boot loader:

        cd /boot/efi/EFI

        cp -R ubuntu/* BOOT/

        cd BOOT

        cp grubx64.efi bootx64.efi

9. Reboot the system.

----------------------------------------------
https://askubuntu.com/questions/1028703/the-grub-efi-amd64-signed-package-failed-to-install-target#1028709
Orginally Published at 



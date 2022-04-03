# SurfacePro4-FydeOS-SecureBoot
Secure Bootloader for [Brunch ChromeOS](https://github.com/sebanc/brunch) and Surface Pro 4

# Preface
This is a working secure bootloader for Brunch ChromeOS on the Surface Pro 4, based off [this guide](https://github.com/badstorm/surface-pro-7-opencore/blob/master/SecureBoot.With.Grub.md) with a few caveats:
- Need to mount this `Super-UEFIinSecureBoot-Disk_minimal.img` image with Linux using the offset _(found using [parted](https://askubuntu.com/a/236284))_ via this command: `sudo mount -o loop,ro,offset=1048576 Super-UEFIinSecureBoot-Disk_minimal.img /path/to/mount/`, as it can't simply be extracted like described in that guide.

# Instructions
You should be able to copy/replace the entire contents of the `EFI` folder on your EFI Partition with the contents from this repo, but keep the original `Microsoft` folder in place.

Also ensure to copy the `ENROLL_THIS_KEY_IN_MOKMANAGER.cer` certifiate to the root of your EFI partition, and follow the original guide or next section to enroll the key.

Note that this configuration also requires your brunch `chromeos.img` file to exist at the root of one of your partitions.

This also utilizes the latest version of rEFInd for the EFI booloader.

# Add the Key and Boot
Reboot and enable Secure Boot in the BIOS, and boot from the `/EFI/BOOT/BOOTX64.EFI` image _(add a boot entry to your bios using EasyUEFI or some other tool if not present)__

You now get a blue screen with the Access Denied error. Follow these instructions:

- At the error page press OK
- Press any key to perform MOK management
- Select Enroll key from disk
- Select Continue
- Select the disk where you put the .cer file
- Select Yes and then Reboot

You should now be able to boot into Brunch/ChromeOS with Secure Boot enabled!

# Disable AMD GPU on MacBook Pro 2011

## Overview
This guide provides a step-by-step method to disable the faulty AMD GPU on a MacBook Pro 2011 using Arch Linux. The process involves modifying EFI variables to prevent the system from utilizing the discrete GPU, which can resolve boot issues and graphical artifacts.

## Prerequisites
- A USB flash drive (at least 1GB)
- A working PC or Mac to create the bootable USB
- Arch Linux ISO: [Download here](https://www.archlinux.org/download/)
- Rufus (for Windows users): [Download here](https://rufus.ie/)

## Instructions
### Step 1: Create a Bootable USB with Arch Linux
1. Download the Arch Linux ISO from the link above.
2. Use Rufus to create a bootable USB:
   - Select your USB drive.
   - Choose the Arch Linux ISO.
   - Use default settings and start the process.

### Step 2: Boot MacBook Pro from USB
1. Insert the bootable USB into your MacBook Pro.
2. Power on the Mac while holding the `Option` (`⌥`) key.
3. Select the USB drive from the boot menu and press `Enter`.

### Step 3: Modify Boot Parameters
1. When the Arch Linux boot menu appears, press the `e` key to edit boot parameters.
2. Navigate to the end of the boot line using the right arrow (`→`) key.
3. Append `nomodeset` at the end of the line.
4. Press `Enter` to boot Arch Linux.

### Step 4: Modify EFI Variables to Disable AMD GPU
Once Arch Linux has booted successfully, execute the following commands:

```bash
cd /sys/firmware/efi/efivars
chattr -i gpu-power-prefs-fa4ce28d-b62f-4c99-9cc3-6815686e30f9
rm gpu-power-prefs-fa4ce28d-b62f-4c99-9cc3-6815686e30f9
printf "\x07\x00\x00\x00\x01\x00\x00\x00" > gpu-power-prefs-fa4ce28d-b62f-4c99-9cc3-6815686e30f9
chattr +i gpu-power-prefs-fa4ce28d-b62f-4c99-9cc3-6815686e30f9
cd /
umount /sys/firmware/efi/efivars
```

### Step 5: Reboot the MacBook
1. Press and hold the power button until the system shuts down.
2. Power it back on; it should now boot using the integrated Intel GPU.

## Notes
- If the process is successful, the MacBook should boot without graphical artifacts.
- If issues persist, ensure Secure Boot is disabled (if applicable) and retry the steps.
- This method is **permanent** unless reversed manually.

## Troubleshooting
- If the system still tries to use the AMD GPU, verify the EFI variable changes.
- If you encounter a "Permission Denied" error, ensure you are using a root shell (`sudo su` or equivalent).
- If the system does not boot, try resetting the NVRAM (`Command + Option + P + R` at startup) and repeat the steps.

## Disclaimer
This procedure modifies system firmware settings. Proceed with caution and at your own risk. The author is not responsible for any damage or data loss.

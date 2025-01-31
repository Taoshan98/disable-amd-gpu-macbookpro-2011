# disable-amd-gpu-macbookpro-2011
Guide to disable broken AMD GPU for MacBook Pro 2011

Look, when you read "[TAB]" it means "press TAB key"


1 - Make a bootable USB with Arch Linux: https://www.archlinux.org/download/ on it using Rufus: https://rufus.ie/

2 - Power on the MacBook holding `option` key and select the USB drive

3 - On Arch Linux's Menu press `e` key and go to the end of the line with the right arrow `->` and write `nomodeset` and Enter

4 - Wait for Arch Linux boot up

5 - Run all the following commands

6 - `cd /sys/firmware/efi/efivars`

7 - `chattr -i gpu-power[tab]`

8 - `rm gpu-power[tab]`

9 - `printf "\x07\x00\x00\x00\x01\x00\x00\x00" > gpu-power-prefs-fa4ce28d-b62f-4c99-9cc3-6815686e30f9`

10 - `chattr +i gpu-power[tab]`

11 - `cd /`

12 - `umount /sys/firmware/efi/efivars`

13 - Press MacBook's power button to reboot

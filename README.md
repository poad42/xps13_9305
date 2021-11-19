# Arch linux for Dell XPS 13 (9305) 2021

## Config
 OS: Arch Linux 

 Kernel: x86_64 Linux 5.15.3-1-ck

 Uptime: 1h 9m

 Packages: 590

 Shell: bash 5.1.8

 Resolution: 1920x1080

 DE: GNOME 41.1

 WM: Mutter

 WM Theme: Flat-Remix-Blue-Darkest-fullPanel

 GTK Theme: Flat-Remix-GTK-Blue-Dark-Solid [GTK2/3]

 Icon Theme: Adwaita

 Font: Ubuntu 15

 Disk: 27G / 485G (6%)

 CPU: 11th Gen Intel Core i7-1165G7 @ 8x 4.7GHz [46.0°C]

 GPU: Iris Xe Graphics

 RAM: 3064MiB / 15735MiB

## What's not working
 Fingerprint scanner, unsupported by dell's package for goodix, openned this forum thread (https://www.dell.com/community/XPS/Fingerprint-scanner-on-linux-with-XPS-13-9305-2021/m-p/8072839#M92118)

## Things that require some work
 While everything mostly works out of the box with the Arch kernel, I decided to run the disk on raid with intel rapid stuff instead of switching to AHCI. This needs the vmd driver to be loaded on boot so that the nvme drive can be mounted.
 This can be done by this https://bugs.archlinux.org/task/68704, but arch now has https://github.com/archlinux/mkinitcpio/pull/60 so future builds/ISOs should support this by default.

 Additional headache with vmd is it needs some ASPM patches on Tiger lake or it doesn't properly suspend. So i made this repo https://github.com/poad42/linux/commits/5.15.3 with these two patches picked and modified linux-ck's pkbuild to use this source (https://github.com/poad42/linux-ck). So probably avoid headaches and switch to ahci? But I got both these stuff sorted and maybe mainline will merge these patches soon and it will all be hunky dory.

 Note that this is an issue on other tiger lake laptops on vmd like the HP spectre for example see https://bugzilla.kernel.org/show_bug.cgi?id=213717 and https://bugzilla.kernel.org/show_bug.cgi?id=215063 (is the one I filed hoping the above patches get merged)

 Sound:
  to fix hissing and headphones to getting picked up on boot add the following below to /etc/modprobe.d/alsa-base.conf

options snd-hda-intel power_save=0 power_save_controller=N

options snd-usb-audio index=-2

options snd-hda-intel position_fix=1

options snd-hda-intel model=,dell-headset-multi

and run 

sudo sh -c 'echo "snd-hda-intel" >> /etc/modules'

## Encryption and secure boot
 I don't use them but secure boot should work if you don't use any external modules and follow arch wiki guide to set it up and encryption as well should work fine.

 ## Conclusion

 On the whole linux runs really well on the laptop, touchpad feels good, everything is super snappy and oh god it boots under 5 seconds with systemd boot. With a minimal gnome install, it will not get in your way. I find it better than the clusterfuck that is windows 11.

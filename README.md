# NanoPC T6 Plus

Collection of notes and experiences trying to use a rk3588 based soc (NanoPC T6 Plus) as an everyday computer.

### tl;dr
> **edk2-rk3588** flashed to SPL (secondary program loader) to replace u-boot spl
> **grub-efi** for booting with specfic device-tree file **rk3588-nanopc-t6-lts.dtb**
> **ubuntu-rockchip** image using **rockchip-vaapi** for system-wide video acceleration

This setup gave me the best overall desktop experience using the NanoPC T6 Plus.  I use it everyday for browsing the internet and watching streaming or local media, basic computing and most daily computer tasks. I have even compiled kernels sucessfully.  It runs a frigate nvr container 24/7 with hardware ai detection and even hosts an isolated hotspot for the wirelesss ip cameras.  All while I watch 4k media. There still are some issues.

### Initial Goals...
- Lowest powered [watts] modern desktop I can effectively utilize
 - Capable of everyday computer task (e.g. desktop file management, web browser, media player, applications)
 - Playback 4k videos without using cpu (hardware video acceleration)
 - Browse websites and streaming drm [copy protected] video sites (e.g. youtube movies, netflix)

### Choosing the hardware...
  I origianlly was interested in a raspberry pi 5 and possibly some additional hats for extended features since i already owned a 3, 4, and a pico.

 - raspberry pi 3 for a emonpi, a diy home power monitor
 - raspberry pi pico w as a universal print server
 - raspberry pi 4b for a soc desktop pc, but end up using for a Home Assistant hub
  
The 4b's desktop performance was unsatifactory, so I ended up repurposing the 4b for a  "Home Assistant" server which worked out great. I figured the next logical step up was a pi 5. Searching online for information on linux desktops on rpi5 I was lead to armbian.com and their pre-built system images and conviently there are support ranks! I wonder what rpi's are? Standard? I expected a higher rank since they are so common.  Well there are 20 "platinum" supported boards so ultimately I choose the NanoPC T6 LTS which is platinum ranked and had the following features.

 https://armbian.com/boards?support=platinum https://wiki.friendlyelec.com/wiki/index.php/NanoPC-T6_Plus

 - Advertised to support fully gpu and vpu hardware acceleration
 - 8k video playback, and hdmi out supporting 8k
 - dual 2.5g ethernet
 - usb-c with display out support
 - m.2 for wireless (not included)
 - m.2 slot for nvme (nvme not included)
 - headphone jack
 - built in hdmi input upto 4k 60hz

Sidenote: The listing I purchased the NanoPC T6 LTS had the option to get a 16gb upgraded version for only $30 more, but turns out that changed its model from the "LTS" model to the "PLUS", which is only ranked with "standard" supported on armbian.com.  From what I am reading on the NanoPC Wiki it looks like it may just be a variation of the LTS with more ram and some slight superficial design changes.
https://wiki.friendlyelec.com/wiki/index.php/NanoPC-T6_Plus#Differences_Between_NanoPC-T6_LTS_and_NanoPC-T6_Plus

Official NanoPC T6 images https://wiki.friendlyelec.com/wiki/index.php/NanoPC-T6_Plus#Official_image
Armbian images for PLUS https://armbian.com/boards/nanopct6-plus
Armbian images for LTS https://armbian.com/boards/nanopct6-lts

### First impressions of official/armbian images...
  -tried android tv, debian/ubuntu images, android tv was worst than expected so linux only from now on
  -official images requires custom chromium browser for video acceleration, I want to use what "I" want
  -chromium: switching to another windows that covers the browser while watching a video in the browser breaks playback when trying to return back to playing browser window
  -8k video playback does not work for all players only mpv, gst-player works but is not usable for normal users
  -hardware support varies for each image (e.g. missing  usb2ports, bluetooth issues, headphone detection)

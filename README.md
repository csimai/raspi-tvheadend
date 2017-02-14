# About

This document provides the build options and installation instructions for **tvheadend 4.1-2426** (considered unstable as of this writing) for the Rasberry Pi.  The repository contains the prebuilt .deb archive for **OSMC 2017.02-2** (Pi B/Zero).

The general build process is presented but is not needed to install on OSMC 2017.02-2.  However, it could be of some value as a guide where OS's other than OSMC are used on the RasPi B/Zero. 

# Motivation

I could not use my usb DVB-T (August T202, August T205 and Avermedia Volar Green) tuners with the most recent stable version of tvheadend 4.09 that is supplied with the latest version of OSMC.  I could get w_scan to work but then tvheadend would not recognize the device.  There appear to be a number of OSMC forum threads on this issue with suggested solutions.  In my case the tvheadend version 4.1-2426 is now working well on my Raspberry Pi B and the usb DVB-T devices are recognized.  I am using the August T202 device.

# OSMC Version

This is the **OSMC 2017.02-2** release installed from image **OSMC_TGT_rbp1_20170210.img.gz**.  This can be obtained by:

    $ sudo wget http://download.osmc.tv/installers/diskimages/OSMC_TGT_rbp1_20170210.img.gz

Then unpack and burn the image to your preferred device with dd.  This procedure is outside the scope of this document.

# Kernel Version

The kernel version for this OSMC (RasPI) release is:

    $ uname -a
    Linux osmc 4.4.27-7-osmc #1 SMP PREEMPT Tue Jan 24 03:38:31 UTC 2017 armv7l GNU/Linux

# DVB-T Device

I am using the inexpensive but excellent **August T202 DVB-T** device.  The firmware for this tuner is:

    dvb-usb-it9135-02.fw
    dvb-usb-af9035-03.fw

To identify other USB DVB-T/T2 firmware, see https://www.linuxtv.org/wiki/index.php/DVB-T_USB_Devices.

# Building

Building is optional as it can be installed with the provided .deb archive - this section is given for the purpose of completelness and can be skipped (see section **Installation** below).  However for those interested the build was done on a Rasberry Pi B and the tvheadend source for this build can be obtained from https://github.com/csimai/tvheadend.  To access and build it, do:

    $ git clone https://github.com/csimai/tvheadend.git
    $ cd tvheadend
    $ sudo AUTOBUILD_CONFIGURE_EXTRA="--disable-ffmpeg_static --disable-libvpx_static --disable-libtheora_static --disable-libvorbis_static --disable-libfdkaac_static" ./Autobuild.sh

or alternatively (untried but according to irc #hts this will also work):

    $ sudo AUTOBUILD_CONFIGURE_EXTRA="--disable-ffmpeg_static" ./Autobuild.sh

There will be a lot of dependencies to install, and the procedure will stop until each of these are satisfied - this process to completion will probably take 4 or 5 hours with the related builds and package installations.  The final .deb archive products will be:

    tvheadend_4.1-2426~gef89ef8_armhf.deb
    tvheadend-dbg_4.1-2426~gef89ef8_armhf.deb

# Installation

Dependencies are:

    libavahi-client3 (>= 0.6.16)
    libavahi-common3 (>= 0.6.16)
    libc6 (>= 2.14)
    libdbus-1-3 (>= 1.0.2)
    libssl1.0.0 (>= 1.0.0)
    liburiparser1 (>= 0.6.0)
    zlib1g (>= 1:1.1.4)

So do:

    $ sudo apt-get install \
    zlib1g \
    libc6 \
    libssl1.0.0 \
    libdbus-1-3 \
    liburiparser1 \
    libavahi-common3 \
    libavahi-client3

**Important:**  if the tvheadend 4.09 is already installed, go to the OSMC App Store and uninstall it and move directory `/home/osmc/.hts` to `/home/osmc/.hts_old`.  Then do:

    $ sudo dpkg -i tvheadend_4.1-2426~gef89ef8_armhf.deb

When everything has installed well and tvheadend is set up then `/home/osmc/.hts_old` can be removed.

That's it!

# Warranty and License

There is no expressed or implied warranty for this software.  Use it entirely at your own risk.  The License is that of the tvheadend software which is currently GPLv3 with the intent to license as GPLv2 in future. 

# Acknowledgements

I thank the (separate and independent) development teams of tvheadend and osmc for their excellent work.  Please contribute to their efforts by **donating**.  Donations can be made as follows:

- https://tvheadend.org/projects/tvheadend/wiki/Donate
- https://osmc.tv/blog/#donate

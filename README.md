# rcraid-dkms (Proxmox fork)
AMD RAIDXpert driver as DKMS package

Foreword:
===========

Many AMD mainboards for the AM4 socket based on the following chipsets come with RAID support:
 * X370
 * X399
 * X470
 * X570

But this RAID mode, which needs to be set in the BIOS, requires a specific driver for each OS.
There is a driver for Windows, but for Linux AMD provides either a binary blob or the sources.
When following the instructions, you will need to recompile the driver and install the kernel module on each kernel update and/or upgrade.
Since we are in the 21 century and we have software like DKMS, we don't need to do this manually, but let it happen automatically.

Goal
====
Therefore we try here to keep the code alive for many kernel versions as possible and deliver it within a PPA for Ubuntu as a DKMS package.

Installation
============
  * Driver package for Ubuntu: https://launchpad.net/~thopiekar/+archive/ubuntu/rcraid 
    ```bash
    sudo add-apt-repository ppa:thopiekar/rcraid
    sudo apt-get update
    sudo apt-get install rcraid-dkms
    ```
  * Switching to RAID mode:
    * Boot Linux in AHCI mode.
    * Append `modprobe.blacklist=ahci` to GRUB_CMDLINE_LINUX_DEFAULT in /etc/default/grub
    * Run `sudo update-grub`
    * Restart
    * Switch to RAID mode
    * Boot your Linux installation from a RAID disk

Thanks go to..
==============
  * To AMD to hand out the driver as source code at least. (Some history: Just think about Intel Poulsbo..)
    * https://www.amd.com/en/support/chipsets/amd-socket-am4/x370 - section Linux
  * To Martin Weber (@martinkarlweber) for sharing patches to make the driver work on Linux >= 4.15.x
    * https://github.com/martinkarlweber/rcraid-patches

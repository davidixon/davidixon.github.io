---
layout: post
title: "Fixing snapd in Hyper-V's pre-built Ubuntu virtual machines"
date: 2019-09-01 12:45
---

For some time now, Microsoft and Ubuntu have offered pre-built [optimized versions of the operating system for Hyper-V](https://blogs.windows.com/windowsdeveloper/2018/09/17/run-ubuntu-virtual-machines-made-even-easier-with-hyper-v-quick-create/) that you can quickly create with support for *enhanced sessions* built right in. It's so much quicker than manually creating a virtual machine, installing Ubuntu and then installing and configuring things to get better performance, higher display resolutions and clipboard integration with your host machine.

Unfortunately, I've noticed that the pre-built images for Ubuntu 18.04.2 and 19.04 have been somewhat broken for at least the last month or two, [perhaps longer](https://bugs.launchpad.net/ubuntu/+source/livecd-rootfs/+bug/1828500). When trying to run Software Updates (or manually using *sudo apt upgrade* in the terminal), things would eventually get stuck due to issues with 'snapd' process.

The last time I ran into this issue, I just trashed the virtual machine and just manually did everything myself [following Microsoft's guide](https://github.com/Microsoft/linux-vm-tools/wiki/Onboarding:-Ubuntu). But I had to create a new virtual machine for something today and decided to try using Microsoft's pre-built Ubuntu 18.04.2 virtual machine and ran into this issue again.

This time, I decided to do a bit more googling and discovered it's relatively simple to fix.

After quick-creating the virtual machine in Hyper-V, connecting, and logging in to it, open the Terminal application and run these commands:

> sudo rm -r /var/cache/snapd/aux
>
> sudo apt purge snapd
> 
> sudo apt install snapd
> 
> sudo snap install core

Then, after restarting the virtual machine, updating the system through Software Updates or the terminal should now be working perfectly again.

Hopefully, Microsoft and/or Ubuntu fix this issue with the next pre-built images they release, presumably for version 19.10.

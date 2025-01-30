# Prerequisites

## Hardware

The parts list I'll be using are:

1. 6x Raspberry Pi CM5. Specifically, I'm using the CM5 Lite with 8GB RAM and no WiFi
2. DeskPi Super6C + Case
3. 6x SD cards

If you want to include local storage, you can also include an NVMe drive for each module.

## Software

I'm not going to focus too much on operating systems right now. Originally I wanted to use MicroOS but it doesn't
support CM5's at time of writing (2025-02-01) so for now I'm settling on the Debian-derivative Raspberry Pi OS.
Ultimately this is a guide about Kubernetes, and the host operating system matters less. If I do get MicroOS working,
I'll revisit this portion of this writeup as I believe there's some interesting aspects about the host OS that's worth
talking about.

## Next

Next, we need to [setup our hardware.][hardware-setup]

[hardware-setup]: ./02-hardware-setup.md

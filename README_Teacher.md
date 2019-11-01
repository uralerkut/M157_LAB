 https://github.com/uralerkut/M157_LAB 

# Version for teachers

# RetroPie

``` bash
Version 1.2
```
This .md got created by
``` bash
Kevin Linh | Ural Erkut
```

# Table of Contents
1. [Intro]
2. [Requirements]
3. [Preparing your Pi]
4. [Installing RetroPie on top of Raspbian]
5. [Installing FTP for ROM transfer]
6. [PLAY!]
7. [MODS!]
8. [Bibliography for teachers]


## Intro

RetroPie is a fantastic Linux distribution to turn your Raspberry Pi into a fully featured game console and computer emulator. RetroPie runs Emulation Station and supports all major retro video game emulators, allowing you to play games from the NES, SNES, Genesis, Atari, and more on your Pi, thus becoming your own Raspberry Pi emulator.
This README aims to guide users in installing RetroPie on their Raspberry Pi on top of Raspbian. 

The ROMs (games) needed for the RetroPie, can be downloaded from this following link:
https://www.downloadroms.io/

## What is an emulator?

An emulator is software that makes a computer behave like another computer, or in the case of RetroPie a computer that behaves like a video game console such as the Super Nintendo. The RetroPie SD image comes pre-installed with many different emulators. Additional emulators may be installed from within RetroPie. 

![Capture](https://cloud.githubusercontent.com/assets/10035308/22178094/cf801644-dfe2-11e6-8327-71a61d540d2f.png)

## What is a ROM?

ROMs are digital versions of game cartridges. Loading up a ROM in an emulator is the equivalent of putting a cartridge in a game console.

ROMs are copyrighted content and as such are not included with RetroPie. 

![Capture](https://cloud.githubusercontent.com/assets/10035308/22178090/cf5cad76-dfe2-11e6-8c63-ec48cc4755f6.png)





## Requirements Hardware


| What             | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| Pi               | Raspberry Pi (A, A+, B, B+, 2, Zero, 3 or 4) - for best performance use a Raspberry Pi 3 Model B+ or the new Pi 4 |
| MicroSD Card     | For the distribution and ROM games. (GB minimum in storage capacity.) |
| Screen           | You need to see the games in order to play, right? |
| Wifi or Ethernet | Self-evidently for this project|
| Keyboard         | You can use a keyboard or a conroller via USB to play |
| Patience         | Do not worry it will be worth the effort |

## Requirements Software


| What             | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| Raspbian         | The easiest OS to install RetroPie onto: https://www.raspberrypi.org/downloads/raspbian/ |
| Retropie         | The latest RetroPie image from: https://retropie.org.uk/download/  |
| Game ROMs        | Games have to be downloaded from: https://www.downloadroms.io/ |


## Preparing your Pi 

(you can skip this part if you have an OS installed on your Pi already)

For the basic of things, it is recommended to install an OS first before approaching to anything else. Well ironically, you cannot do that anyway.
Raspbian is a Linux distribution specially made for the Pi. Download balenaEtcher. You will need this to write the .img onto the SD card. Boot it up and follow the instructions as usual.
https://www.raspberrypi.org/downloads/raspbian/
https://www.balena.io/etcher/


## Installing RetroPie on top of Raspbian

This guide is a manual process to recreate the stock SD image RetroPie released on the RetroPie website for the Raspberry Pi. 
Most of the install scripts will attempt to install a variety of packages and libraries that each emulator requires. These installations will fail if your system locale settings are invalid. You can easily verify this by executing locale command. A valid locale will return values set for all options, such as in the example below.

```bash
LANG=en_US.UTF-8
LANGUAGE=en_US:en
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=en_US.UTF-8
```

If any of the above configuration lines are unset (particularly LANG, LANGUAGE, and LC_ALL), you should set them before installing RetroPie. The easiest way to set each item is to use the 
```bash 
update-locale command

```
such as 
```bash 
$ sudo update-locale LC_ALL="en_US.UTF-8"
```

Users can also set the locale through the 
```bash
 raspi-config
```
 tool.


A reboot is required before these changes will be reflected by the 
```bash
 locale
```
 command.

After that, we install the needed packages for the RetroPie setup script:

```bash
sudo apt-get install git lsb-release
```

Then we download the latest RetroPie setup script with
```bash
    cd
    git clone --depth=1 https://github.com/RetroPie/RetroPie-Setup.git
```

The script is executed with
```bash

    cd RetroPie-Setup
    chmod +x retropie_setup.sh
    sudo ./retropie_setup.sh
```
The screen should look like this then:

![Capture](https://cloud.githubusercontent.com/assets/10035308/16218285/f06f3ba8-3738-11e6-9ccc-be601172713b.png)

### Full install
This will install the core and main packages which are equivalent to what is provided with the RetroPie SD image.

Now, you have to copy your rom files into the ROMs directory. If you followed the steps above the main directory for all ROMs is ~/RetroPie/roms (or /home/pi/RetroPie/roms, which is the same here). In this directory there is a subdirectory for every emulated system, e.g., nes, snes, megadrive. Attention has to be taken for the extensions of the ROM files. 

EmulationStation can be run from the terminal by typing 
```bash
    emulationstation
```
in the terminal in order to start RetroPie.

## Installing FTP for transferring ROMs

If you wish to use wifi to transfer roms over the network rather than a USB stick or ethernet cable you will need to setup your wifi- which can also be done from the Retropie menu in emulationstation:



![Capture](https://cloud.githubusercontent.com/assets/10035308/16217941/92b08b8c-3735-11e6-8f20-5d1550af0882.png)

Once configured, you will see your IP address on the top left. You will need to enter this and your Pi its name in order to connect and transfer games to it.

![Capture](https://cloud.githubusercontent.com/assets/10035308/16217944/92cb07fa-3735-11e6-9239-66fba394c669.png)

### Enable SSH

Before we install  a SFTP client however, we need to make sure that SSH is enabled.
SSH stands for secure shell. You can remotely connect to the raspberry pi terminal with an SSH client. A popular ssh client is WINSCP for Windows.

**bash Launch Raspberry Pi Configuration from the Preferences menu.
Navigate to the Interfaces tab.
Select Enabled next to SSH.
Click OK.**

Now SSH is enabled. Reboot.

### For windows users
Simply download and install WINSCP on your windows machine and connect to your Pi with the coresponding credentials of yours.
https://winscp.net/eng/download.php

### For mac users
Follow the same procedure, but with a different program called 
```bash
 Cyberduck
```
https://cyberduck.io/?l=en



![Capture](https://cloud.githubusercontent.com/assets/10035308/12865832/7d9afb68-cc75-11e5-81b2-4529991e1821.png)

You can also use your raspberry pi its ip address instead of 

```bash
 retropie
```

**Some common terminal commands:**

**Reboot:**


```bash 
sudo reboot
```
**Shutdown:**


```bash
 sudo shutdown -h now
```
**Change Directory**


```bash
 cd /path/to/directory
```
**list Files in Current Directory**


```bash
 ls
```
**Retropie Setup Script:**


```bash
 sudo /home/pi/RetroPie-Setup/retropie_setup.sh
```
**Edit Files with Nano:**


```bash
 sudo nano /path/to/file.txt
```
**Change owner to Pi:**


```bash
 sudo chown pi:pi filetobechanged
```
**Change owner of folder and all files in folder to Pi:**


```bash
 sudo chown -R pi:pi /folder/to/be/changed
```
**Make shell script executable:**


```bash
 sudo chmod +x yourshellscript.sh
```

After that, drag&drop your ROM file into the appropriate emulator folder.

## PLAY!
After you've added your roms you need to restart emulationstation in order for them to show up. You can restart
 ```bash 
emulationstation
 ```
from the start menu, or by rebooting your pi with 
```bash 
sudo reboot
```
or via the physical power button.

You can either play with a keyboard (you probably already set that upon installing RetroPie) or dedicated supported controllers and as such.![Capture](https://cloud.githubusercontent.com/assets/10035308/22185414/f129dc28-e099-11e6-8524-93facf275eda.png)



![Capture](https://cloud.githubusercontent.com/assets/10035308/22185415/f12ff342-e099-11e6-8adb-d18e9c638e94.png)

![Capture](https://cloud.githubusercontent.com/assets/10035308/22185413/f10f27de-e099-11e6-97a4-ecbbc82c9e46.png)

## MODS!

### Improving FPS
The display communicates with the Raspberry Pi via SPI, a serial communication bus which is quite slow by default, resulting in very low framerates. Fortunately, we can increase Raspberry Pi its SPI speed to solve this. Get into the console and edit the 
```bash 
/boot/config.txt
```
file with the following command:

```bash 
sudo nano /boot/config.txt
```

Find the line that looks like this:
```bash 
dtoverlay=waveshare32b:rotate=270
```
And modify it so it looks like this:
```bash 
dtoverlay=waveshare32b:rotate=270,speed=80000000,fps=60
```
Then reboot.

### Overclocking your Pi

Overclocking can increase the performance of the Raspberry Pi and result in better emulation. Fortunately, overclocking your Pi is pretty painless. If you have a Raspberry Pi 1 or 2, overclocking is super simple with the built-in overclocking tool. Just pull up the Emulation Station menu and select “Overclock.” After the warning, you will see the overclocking settings that are available. Choose the one you prefer, and that is it.

![Capture](https://www.maketecheasier.com/assets/uploads/2018/09/rpi-overclock-preset.jpg)

Overclocking on the Raspberry Pi 3 or Zero can be done; however, it is a little more hands on. Instead of selecting an option from a menu, you will have to manually overclock. This is done by editing the 
```bash
/boot/config.txt
```
file in the boot directory. It sounds complicated, but it is really not. Finally, be aware that overclocking your Pi can cause it to overheat.

Parameters are set like:

```bash
parameter=value
```

For example, to set the ARM to 1000MHz:
```bash
arm_freq=1000
```

The following speed parameters can be set:

**speed of the ARM core**


```bash 
arm_freq
```
**speed of GPU processor core**


```bash
 core_freq
```
**speed of all GPU components**


```bash
 gpu_freq
```
**speed of SDRAM**


```bash
 sdram_freq
```
**a set of SDRAM timings**


```bash
 sdram_schmoo
```
**voltage of ARM and GPU**


```bash
 over_voltage
```
**voltage of all SDRAM parts**


```bash
 over_voltage_sdram
```

 The voltage starts at 1.2V and adjusts up or down in 0.025V steps. 0 is equal to 1.2V, the minimum -16 is 0.8V, and the maximum 8 is 1.4V. Voltage starts to help when running core/GPU/SDRAM at or over 500MHz.

To set voltage greater than 6 you must set force_turbo=1 which voids the warranty.

An example of clock speeds of a Pi 3

``` bash
total_mem=1024
arm_freq=1300
gpu_freq=500
core_freq=500
sdram_freq=500
sdram_schmoo=0x02000020
over_voltage=2
sdram_over_voltage=2
```



## FAQ

### Why do some emulators not show up?

The RetroPie SD image only ships with the most common emulators, if a system you want is missing you first need to make sure that emulator is installed. The details for installing additional emulators is explained on the [first installation page](https://retropie.org.uk/docs/First-Installation#installing-additional-emulators--ports)

If the system still doesn't show up in Emulation Station, only emulators with ROMs inside its respective folder will show up in the EmulationStation GUI (given that the specific emulator is installed). For example, for the Nintendo 64 emulator to show up, you must have at least one ROM in the `~/RetroPie/roms/n64/` folder. For ROM types supported by each emulator, go to the wiki page for that specific system/emulator.

### Why can't I SSH as root anymore?

The root password is disabled by default (as is the case for Raspbian and many other linux distros).

before setting a root password, the following must be edited

```
sudo nano /etc/ssh/sshd_config
```

look for

```
#PermitRootLogin without-password
```

change it to

```
PermitRootLogin yes
```

then ctrl+x to save,

next set your root password:

```
sudo passwd root
```

restart your Pi to register your changes

see these posts for more details:

https://www.raspberrypi.org/documentation/linux/usage/root.md

http://elinux.org/R-Pi_Troubleshooting#I_don.27t_know_the_root_password

### Reset ownership/permissions of /home/pi/RetroPie roms

To reset all your rom file ownerships back to the "pi" user, enter the [RetroPie-Setup Script](https://github.com/retropie/retropie-setup/wiki/Updating-RetroPie)

navigate to **Configuration / Tools >> resetromdirs**

### Where did the desktop go?

The PIXEL (formerly LXDE) desktop environment was removed from the RetroPie image to keep it smaller.

It can easily be installed from the [RetroPie Setup Script](https://retropie.org.uk/docs/Updating-RetroPie)

in **Configuration / Tools >> Raspbiantools >> Install Pixel Desktop Environment**

after installation it will be accessible from the ports menu of EmulationStation or can be called from the command line with `startx`

![raspbian](https://cloud.githubusercontent.com/assets/10035308/19827420/347e1d6a-9d5e-11e6-8146-d814c8dd087b.png)

You can also install it manually with:

```
sudo apt-get install --no-install-recommends lxde
sudo apt-get install xorg raspberrypi-ui-mods rpi-chromium-mods
```

And then you can access it from the terminal by typing in

```
startx
```

After installation your pi will boot into the desktop environment, you can change the behaviour to boot into emulationstation by selecting the autostart option for emulationstation from the configuration/tools section of the setup script, or you can set the autologin to console option from the boot options of the raspi-config menu.

Note that failing to run startx after the installation may prevent other XWindow-based applications from starting (e.g. Micropolis port), so do launch the desktop after installation to ensure that it is fully set up.

### How do I boot to the desktop or Kodi?

In retropie setup script>>Configuration / tools>>autostart

![autostart](https://cloud.githubusercontent.com/assets/10035308/15987124/7699dbcc-2fda-11e6-8a1f-902e3177d782.png)

- **Start EmulationStation at Boot:** Boots into EmulationStation.
- **Start Kodi at Boot:** Boots into Kodi- if you exit Kodi you will be returned to EmulationStation.
- **Manually Edit /opt/retropie/configs/all/autostart.sh:** you can manually add other programs to start on boot.
- **Boot to text console (autologin):** Boots into the terminal.
- **Boot to Desktop:** If you have a desktop environment installed like LXDE this will boot into the desktop. Note you'll want to disable the retropie splash from the setup script first.



## Bibliography

https://www.downloadroms.io/

https://www.raspberrypi.org/downloads/raspbian/

https://retropie.org.uk/download/

https://www.hackster.io/dmitry21/retropie-full-guide-for-raspberry-pi-gaming-machine-86f0ee 


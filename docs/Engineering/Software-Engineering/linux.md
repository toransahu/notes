<h1>Linux</h1>

[TOC]

# Bash Scripting

## AWK
https://www.gnu.org/software/gawk/manual/gawk.html

## include/source/import 

https://gist.github.com/toransahu/0a816af786b7d0b98ab1e7079bf0426f

## String Comparison
- use `=` or `==`
- keep proper square spacing between operators & brackets (most imp)
- use `double quote` for strings and variables
- sometime we need to use brackets to access env variables

https://gist.github.com/toransahu/4fd3abc369bb5c8a1ee424af07cb1563

### Sub-String Comparison
```bash
string="$(hostname)"
substr="mint"
if [ -z "${string##*$substr*}" ]; then
```

https://gist.github.com/toransahu/f812260a37947a299c5c26adddfa4cfa

## If, elif, else, fi
- Source: https://ryanstutorials.net/bash-scripting-tutorial/bash-if-statements.php


## Switch Case
https://www.shellscript.sh/case.html

--------------------------------------------------

# UNIX Commands

## mv all files/dir to a subdir

BASH

- https://askubuntu.com/questions/91740/how-to-move-all-files-in-current-folder-to-subfolder

```

```

TODO: zsh

```
setopt extended_glob
mv 
```


## [Get System Informations](https://www.tecmint.com/commands-to-collect-system-and-hardware-information-in-linux/)

## Set deafult shell
```
sudo chsh -s /bin/zsh
```
then logout

[In Github:linux-tweaks/guides](https://github.com/toransahu/linux-tweaks/tree/master/guides)

## xclip
```bash
xclip -sel clip <file>
```

## ls prefixed commands
ls           lsA          lsblk        lscpu        lshw         lsipc        lslogins     lsof         lspcmcia     lss16toppm   lsusb        
lsa          lsattr       lsb_release  lsdiff       lsinitramfs  lslocks      lsmod        lspci        lspgpot      lss3   


## find
```bash
find <dir> <type> <test> <expression> <action>

find /Ray/ -type f -name "*.pyc" -delete
```

## Set hostname
### 1. at /etc/hosts
`127.0.1.1    mint-ThinkPad-L440`

### 2. at /etc/hostname
write `mint-ThinkPad-L440`

### 3. then tell the machine
```bash  
sudo hostname mint-ThinkPad-L440
```  

## CPU Info
```bash

cat flags /proc/cpuinfo

```


## CPU Temperature
```bash  
sudo apt-get install lm-sensors 
```   
After installation type the following in terminal  
```bash   
sudo sensors-detect
```  
You may also need to run
```bash  
sudo service kmod start
```  
It will ask you few questions. Answer Yes for all of them. Finally to get your CPU temperature type sensors in your terminal.  
```bash  
sensors
```

## IP Related
- ifconfig
- ip addr
- hostname -I

## ssh
```bash
ssh pi@192.168.1.108
```

### In case of AWS EC2 SSH
Connection freezes frequently on inactivity
- source https://www.quora.com/Why-does-ssh-to-amazon-ec2-instance-gets-frozen-after-sometime
- Solution
    - sudo vim /etc/ssh/ssh_config
        - add TCPKeepAlive yes
        - add ServerAliveInterval 5  where 5 is minute
    - sudo service sshd restart

## sftp
```bash
sftp pi@192.168.1.108


put local_file



get remote_file

```
files will upload/download @ home

## sshfs
```bash

sudo mkdir /mnt/pi


sudo sshfs -o allow_other  pi@192.168.1.108:/ /mnt/pi/
```

## Device connected to the Network
```bash
nmap -sP 192.168.1.0/24
```


## dd (Disk Dump) commands
### Create a backup
`
dd if=/dev/sda of=/opt/backup_sda.img
`

### Restore a backup
`
dd if=/opt/backup_sda.img of=/dev/sda
`

### Clone a hard disk
`
dd if=/dev/sdb of=/dev/sdc
`

### Transfer a disk image
`
dd if=/dev/sdb | ssh root@target "(cat > backup.img)"
`

### Create an iso image of a CD/DVD
`
dd if=/dev/cdrom of=cdimage.iso
`

### Burn an iso image of a CD/DVD
`
dd if=cdimage.iso of=/dev/cdrom obs=32k seek=0
`

### Rescue a file that contains bad blocks
`
dd if=movie.avi of=rescued_movie.avi conv=noerror
`

### Create your own bootloader
`
dd conv=notrunc if=bootloader of=qemu.img
`

### Create a backup of your MBR
`
dd if=/dev/sdb of=mbr_backup bs=512 count=1
`

### Restore a backup of your MBR
`
dd if=mbr_backup of=/dev/sdb bs=512 count=1
`

### Mount dd image of and entire disk
**You must use the start number of the partition.**
`
fdisk -u -l disk_image
`

```bash
Disk /mnt/storage/disk_image: 0 MB, 0 bytes255 heads, 63 sectors/track, 0 cylinders, total 0 sectors
Units = sectors of 1 * 512 = 512 bytesDisk identifier: 0x41172ba5

Device                      Boot    Start    End       Blocks   Id  System
/mnt/storage/disk_image1            63       64259     32098+   de  Dell Utility
/mnt/storage/disk_image2    *       64260    78108029  39021885 7   HPFS/NTFS

Partition 2 has different physical/logical endings:phys=(1023, 254, 63) logical=(4861, 254, 63)
```

Then take the start of the partition that you want to edit, `64260` (disk_image2) in this case, and multiply it by `512`

Ex: `512 * 64260 = 32901120`

`
mount -o loop,offset=32901120 -t auto /mnt/storage/disk_image /mnt/image_partition_2
`

### When the hard disk has errors
**Get the dd_rescue tool**
`
dd_rescue /dev/sdb /opt/backup_sdb.img
`

### Network Clone
- Destination:
`
nc -l -p 2222 | dd of=/dev/sda bs=16M
`

- Source:
`
dd if=/dev/sda bs=16M | nc Destination 2222
`

### Network speed test
`dd if=/dev/zero bs=1M count=100 | ssh user@machine 'cat > /dev/null'
`

## Links
 - Symbolic link
 `ln -s original link`
 
 - Hard Link
 `ln original link`
 
## Task Autorun/Automation

- src1 : https://developer.toradex.com/knowledge-base/how-to-autorun-application-at-the-start-up-in-linux

### Daemons

### Shells

### Graphical

### Cron Jobs

#### Intro
The cron service (daemon) runs in the background and constantly checks the /etc/crontab file, and /etc/cron.*/ directories. It also checks the /var/spool/cron/ directory.

[Source](https://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/)

- create cron job
    - `crontab -e` and edit the opened file
        - add your task (in cron format)
    - or, create a new cron job under `/etc/cron.*/`
        - add your task (in cron format)

#### Syntax
```bash
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=""
1 2 3 4 5 /path/to/command arg1 arg2
# or  
1 2 3 4 5 /root/backup.sh`  
```

- to automate tasks based on time like
    - on boot: @reboot
    - hourly: @hourly or “0 * * * *”
    - daily : @daily or @midnight or “0 0 * * *”
    - weekly: @weekly or  “0 0 * * 0”
    - monthly: @monthly or “0 0 1 * *”
    - yearly: @yearly or @annually or  “0 0 1 1 *”
    
    
    * * * * * command to be executed  
    - - - - -  
    | | | | |  
    | | | | ----- Day of week (0 - 7) (Sunday=0 or 7)  
    | | | ------- Month (1 - 12)  
    | | --------- Day of month (1 - 31)  
    | ----------- Hour (0 - 23)  
    ------------- Minute (0 - 59)  
    
#### Operations
- start: `sudo service cron start`
- stop: `sudo service cron stop`
- restart: `sudo service cron restart`
- status: `sudo service cron status`
- list: `crontab -l` or `crontab -u USERNAME -l`
- delete all: `crontab -r` or `crontab -u USERNAME -r`

#### Type
- System Level
    - need to define USERNAME
    - `1 2 3 4 5 USERNAME /path/to/command arg1 arg2`
- User Level
    - by default takes USERNAME of creator
    - `1 2 3 4 5 /path/to/command arg1 arg2`
    
#### Operators
- asterisk (*)
    - every [minute/hour/day/month/day of week]
- comma (,)
    - list of values
    - like, on this days: 1,2,3,4,5
- dash (-)
    - range
    - like, on this days: 1-5
- seperator (/)
    - stepper
    - like, */2 in hour field means: every 2 hours

#### misc
- print names of all valid files: `run-parts --list /etc/cron.d`
- print script names which would run, but don't run them: `run-parts --test /etc/cron.d`

### Services

### .desktop file
- Works on boot
- put <name>.desktop file with some script in `~/.config/autostart/`
- write script like
    ```bash
    [Desktop Entry]
    Type=Application
    Exec=sh /home/toran/Applications/linux_tweaks/LowBatterySound/LowBattery.sh
    X-GNOME-Autostart-enabled=false
    NoDisplay=false
    Hidden=false
    Name[en_IN]=Low Battery Warning
    Comment[en_IN]=Warning sound on battery less than 15%
    X-GNOME-Autostart-Delay=20
    ```
    
### using /etc/rc.local

### using /etc/init.d


## Disk Related

### fdisk
- manupulate disk partition table
- list devices:  `sudo fdisk -l`

### lsblk
- lists block devices

### blkid
- locate/ print block device attributes

### df
- reports filesystem disk space usage

### du
- estimate file space usage
    - Summarize disk usage of the set of FILEs, recursively for directories.
    

## GRUB

### Edit `grub` configs
```bash
vim /etc/default/grub
```

### `grub` update
```bash
sudo update-grub
```

### Reboot into other OS
```
sudo grub-reboot 2
```

-------------------------------------------------------------

# Problems & Solutions


## Make Anaconda Python Default
- put following in `.bashrc` or `.zshrc`
```
# added by Anaconda3 installer
export PATH="/home/toran/anaconda3/bin:$PATH"
```


## If cinnamon freezes

- go to `tty0` or `tty1` using `Alt` + `Ctrl` + `F1` or `F2`
- login
- type `w` and `enter`
- look under `FROM` column, where row is related to `cinnamon session`
- note the value for that cell, in my case its `:0` (with colon)
- note type `export DISPLAY=:0 cinnamon &` and `enter`

## sudo: unable to resolve host Ray: Connection timed out
- Two things to check (assuming your machine is called my-machine, you can change this as appropriate):
- That the /etc/hostname file contains just the name of the machine.
- That /etc/hosts has an entry for localhost. It should have something like:

```bash
 127.0.0.1    localhost.localdomain localhost
 127.0.1.1    my-machine
```
- If either of these files aren't correct (since you can't sudo), you may have to reboot the machine into recovery mode and make the modifications, then reboot to your usual environment.


## nemo context menu "open in terminal" not working
source: https://forums.linuxmint.com/viewtopic.php?t=204933

```bash
gsettings set org.cinnamon.desktop.default-applications.terminal exec mate-terminal
```

## Speedup mouse scroll
Source: https://forums.linuxmint.com/viewtopic.php?t=221526
```bash
sudo apt install imwheel
```
then use `mousewheel.sh` to adjust the speed.

-------------------------------------------------------------


# Utilities

# Multitouch Gesture 
- src: https://github.com/toransahu/libinput-gestures - by bulletmark

```
sudo gpasswd -a toran input
sudo apt-get install xdotool wmctrl libinput-tools
git clone http://github.com/toransahu/libinput-gestures
cd libinput-gestures
sudo ./libinput-gestures-setup install

cd ~/libinput-gestures

#edit the created libinput-gestures.conf:

vim libinput-gestures.conf

#set following:

gesture swipe down  xdotool key ctrl+alt+Up
gesture swipe up    xdotool key ctrl+alt+Down
gesture swipe right xdotool key ctrl+super+Left
gesture swipe left  xdotool key ctrl+super+Right

sudo make install (or sudo ./libinput-gestures-setup install)

libinput-gestures-setup autostart
libinput-gestures-setup start
```




## Battery Monitor
- Source: http://battery-monitor.maateen.me/


## Battery Optimization

### SATA Power Management
- source: https://askubuntu.com/questions/809127/how-to-turn-off-one-of-sata-hdds-installed-in-the-computer-to-save-power

- Using  hdparm utility.
    - It allows you to control your hard drives' power settings, apart from benchmarking and other stuff.

- put the disk into standby mode
    - whenever you access the disk, it should automatically wake up and work back again
```
hdparm -y /dev/sdX
```

- deeper resting mode
    - may need to restart your computer in order to make the HDD work again
```
hdparm -Y /dev/sdX
```

### PowerTop by Intel (Recommanded)
```
sudo apt-get update
sudo apt-get install powertop
sudo powertop --auto-tune
sudo powertop --calibrate
```


### TLP (Emergency)
- Source: https://linrunner.de/en/tlp/docs/tlp-linux-advanced-power-management.html

```
sudo apt install tlp

#restart

#or
sudo tlp start 
```
## Mono

### Install
https://www.mono-project.com/download/stable/#download-lin

### Verify
Source: https://www.mono-project.com/docs/getting-started/mono-basics/
Scripts: 




## Thinkpad Touchpad Middle Button
### Install
```bash
sudo apt install xserver-xorg-input-libinput
```

### Config
- restart
- alter touchpad setting and choose `use multiple fingers` in click actions

## Finger Print Reader
- src: https://launchpad.net/~fingerprint/+archive/ubuntu/fingerprint-gui
### Installation
0. First of all, if you have installed Fingerprint GUI manually before, get rid of it completely. Remove all binaries, shared libraries, any other files and undo all the changes you have made to your system config files (especially to files under /etc/pam.d/).

1. Add this PPA to your sources:
```bash
    sudo add-apt-repository ppa:fingerprint/fingerprint-gui
    sudo apt-get update
```

2. Install the packages:
```bash
    sudo apt-get install libbsapi policykit-1-fingerprint-gui fingerprint-gui
```

3. Log out of your session and log back in (we need the new session defaults to be picked up).

### Uninstallation
```bash
    sudo apt-get install policykit-1-gnome
    sudo apt-get remove fingerprint-gui
```


## ZSH
```bash
sudo apt install zsh
```

### oh-my-zsh
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

#OR

sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```


## VIM 

### Vundle
- VIM plugin manager (VIM + Bundle)
- install from : https://github.com/VundleVim/Vundle.vim
- i.e. git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
#### Using Vundle
- Mention bundle names (as a github repo) in .vimrc file

```bash
Plugin 'VundleVim/Vundle.vim'
Plugin 'morhetz/gruvbox'
Plugin 'itchyny/lightline.vim'
Plugin 'itchyny/vim-gitbranch'
Plugin 'scrooloose/nerdtree.git'
Plugin 'aperezdc/vim-template'
Plugin 'davidhalter/jedi-vim'
Plugin 'editorconfig/editorconfig-vim'
Plugin 'tpope/vim-abolish'
```

- Install using command

```bash
:PluginInstall
```

### VIM as Python IDE
Source: http://chrisstrelioff.ws/sandbox/2016/09/21/vim_and_vundle_on_ubuntu_16_04.html

- ~/.vimrc & ~/.editorconfig config files @ https://gist.github.com/toransahu/66c69903649f3d417d8ba4dc78324f60

- cheat sheet: https://gist.github.com/toransahu/4a921c6fb73274479dbdfbcfe6dda483

## Tmux

### Tmux Package Manager
Source: https://github.com/tmux-plugins/tpm

~/.tmux.conf : https://gist.github.com/toransahu/53a523d973a212f52ce53474417e01b1

### Tmux Plugins:
- Sidebar: https://tmuxcheatsheet.com/tmux-plugins-tools/?full_name=tmux-plugins%2Ftmux-sidebar


### Commands
- abbr.
    - prefix: `ctrl + b`

- help: `ctrl + b ?`

- select, copy, paste within tmux
    - enter scroll mode: `ctrl + b [`
    - enter select mode: `ctrl + space`
    - move cursor to select text
    - copy to tmux buffer: `alt + w`
    - copy to system clip: `ctrl + b - y`
    - paste to any tmux: `ctrl + b ]`
    
- create/split pane    
    - vertical split: `prefix %`
    - hor split: `prefix "`
    
- convert a pane to window: `prefix !`

- move to pane: `prefix arrows`

- close current pane: `prefix x`



### Load .bashrc with tmux

By default tmux runs a login shell. When bash is invoked as an interactive login shell, it looks for ~/.bash_profile, ~/.bash_login, and ~/.profile. So you have to put `source ~/.bashrc` in one of those files.

Another way to solve this issue is to put in your file .tmux.conf the line:

`set-option -g default-shell "/bin/bash"`


## KeyBoard Custom Shortcuts Bindings
### Emulate right click from keyboard
- install xdotool
```bash
sudo apt install xdotool
```

- bind keyboard shortcut with command: `xdotool click 3`



## Backup & Restore Cinnamon settings
```bash
sudo apt install dconf-cli

#backup
dconf dump /org/cinnamon/ > cinnamon_backup

#restore
dconf load /org/cinnamon/ < cinnamon_backup


#reset to default
dconf reset -f /org/cinnamon/
```

---------------------------------------

# Raspberry Pi
## OS
### Raspbian with RPD Desktop 
- prepare
https://www.raspberrypi.org/forums/viewtopic.php?t=135316

### Raspbian Lite (without GUI)

#### Install Desktop for Lite
Source: https://www.raspberrypi.org/forums/viewtopic.php?t=133691

#### Enable ssh & enter SSID/WiFi details without keyboard
Source: https://medium.com/@danidudas/install-raspbian-jessie-lite-and-setup-wi-fi-without-access-to-command-line-or-using-the-network-97f065af722e


### Ubuntu Core/Snap


### Windows IoT

## Display

### Touch Screeen Config
- 5 inch capacitive 800*480

`/boot/config.txt`
```bash
framebuffer_width=800
framebuffer_height=480
hdmi_force_hotplug=1
hdmi_group=2
hdmi_mode=87
hdmi_cvt 800 480 60 6 0 0 0
```


## Backup Image from Burnt Image

### On a different linux PC using USB.
- It won't work on the raspi!, it will get trapped in infinit loop

```bash
#list disk
sudo fdisk -l

#backup SD card
sudo dd bs=4M if=/dev/sdb | gzip > /home/your_username/image`date +%d%m%y`.gz

#restore the backup on SD card
sudo gzip -dc /home/your_username/image.gz | dd bs=4M of=/dev/sdb
```

### In Raspberry Itself using `rsync`


## Network Drive Mount (sshfs)
```bash
#Install SSHFS

sudo apt-get install sshfs

#First, create a directory on your host computer:

mkdir pi

#Then mount the Raspberry Pi's filesystem to this location:

sudo sshfs -o allow_other pi@192.168.1.124:/ pi

#Now enter this directory as if it is a regular folder; you should be able to see and access the contents of the Raspberry Pi:

cd pi/
ls

```

## Remote Audio

### bluetooth

#### Way 1
```
sudo apt-get install bluetooth  blueman bluez python-gobject python-gobject-2 pulseaudio-module-bluetooth

sudo systemctl status bluetooth
pulseaudio --start
```

- https://gist.github.com/mill1000/74c7473ee3b4a5b13f6325e9994ff84c
- https://raspberrypi.stackexchange.com/questions/48140/raspberry-pi-3-connecting-to-bluetooth-audio-device-on-raspbian-jessie
- https://markus.jarvisalo.dy.fi/2017/12/making-the-raspberry-pi-3-a-bluetooth-audio-receiver/

#### Way 2
- https://www.instructables.com/id/Turn-your-Raspberry-Pi-into-a-Portable-Bluetooth-A/
```bash
$ sudo vim /var/lib/bluetooth/00:1A:7D:DA:71:11/config
```

### wifi
- shareport
- https://thepi.io/how-to-set-up-a-raspberry-pi-airplay-receiver/

## enable ssh from card
- put empty ssh file inside /boot/

## set wifi/ssid  from card
- change inside /etc/network/interface

```bash
    auto lo
     
    iface lo inet loopback
    iface eth0 inet dhcp
     
    allow-hotplug wlan0
    auto wlan0
     
     
    iface wlan0 inet dhcp
            wpa-ssid "Connecting..."
            wpa-psk "PrideValencia_A704"
```

## wifi to ethernet

src: https://www.instructables.com/id/Share-WiFi-With-Ethernet-Port-on-a-Raspberry-Pi/

```
sudo apt install dnsmasq -y
cd
wget https://raw.githubusercontent.com/arpitjindal97/raspbian-recipes/master/wifi-to-eth-route.sh
chmod +x ~/wifi-to-eth-route.sh
sudo crontab -e
@reboot bash /home/pi/wifi-to-eth-route.sh &  # add it to crontab file
```

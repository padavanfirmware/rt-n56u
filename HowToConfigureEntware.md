

# How To Configure Routers Asus RT-N56U/RT-N65U For Entware Usage #

---



<a href='http://entware.wl500g.info/'>Entware</a> is an advanced package manager which allows you to easily install, and uninstall cross-compiled Linux applications to your device over the internet. This is <a href='https://openwrt.org/'>OpenWRT</a> software repository, compiled with a fairly modern <a href='http://code.google.com/p/wl500g/'>toolchain</a>. It uses <a href='http://code.google.com/p/wl500g-repo/wiki/Goal'>new features</a>, not available in <a href='http://en.wikipedia.org/wiki/Optware'>Optware</a>.
<a href='http://entware.wl500g.info/binaries/entware/Packages.html'>The list of Entware packages</a> is available.

## Installation and Usage of the Terminal Application ##


First, open your browser, select in the lower left pane <a href='http://my.router/Advanced_System_Content.asp'>Advanced Setting -> Administration -> System</a>
and choose a server you'd like to use. Note, that it is highly recommended to use SSH as the server for external connections only.  Because Telnet is an insecure protocol, and is the very replacement for it.  However, for private (internal) network usage security may not be a necessity.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/adm-system-en.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/adm-system-en.png)

In the above example SSH has been selected as the preferred method. Select the option that you wish to use and then apply to save the settings to the router.

You'll need a <a href='http://en.wikipedia.org/wiki/Terminal_emulator'>terminal client</a> to establish a connection with RT-N56U. The terminal application is a serial computer interface for text entry and display output. There are many different applications. You should choose one by your OS.



### Directions for Windows XP, Vista, and Windows 7 users ###


<a href='http://www.putty.org/'><b>PuTTY</b></a> is a free implementation of Telnet and SSH for Windows and Unix. Download the installer, and install the application.  After installation there is minimal configuration needed to access the router.  To start the session, you will need to enter a few basic parameters. Within the "Session" category select  "Host Name" field, enter _**my.router**_ or _**the IP address of router**_. Select a login protocol to use, from the "Connection type" that matches the protocol configured for the router.  Afterwards, select the Translation category and make sure that UTF-8 is configured for the character set field.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/putty_932x448.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/putty_932x448.png)



---

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **IMPORTANT NOTE: NEVER SAVE YOUR LOGIN AND / OR PASSWORD TO ANY CLIENT WHEN YOU USE TERMINAL CONNECTION!!!**

---



Once you have finished the proper configurations, select the "Open" button at the bottom right of the configuration window, and PuTTY will initiate the connection to the router using the proper protocol.


### Directions for MacOS Users ###

<table>
<tr>
<td width='400'>
Open Finder, and go to Applications => Utilities. Double click on Terminal, or highlight Terminal and Apple/Command Key + Arrow Down.<br>
</td>
<td>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/terminal_in_osx.jpg' />
</td>
</tr>
</table>

```
ssh admin@my.router
```

or use one of the alias names: ```
ssh admin@rt-n56u, ssh admin@my.rt-n56u```


## USB Disk Formatting ##


Linux based systems use [EXTended filesystem](http://en.wikipedia.org/wiki/Extended_file_system). It is recommended to use an external disk (HDD, Flash) that is more than 512MB in capacity, and is formatted with EXT2, EXT3 or EXT4 filesystem. EXT4 is recommended filesystem.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **NOTE: _It is not recommended to use a USB disk that has a larger  than 2TB capacity to avoid driver, and possible data issues. It is possible, but not recommended to use NTFS disks on Linux.  The instructions will be based on the recommended Linux filesystem_**.



### For Windows XP, Vista, or Windows 7 Users ###


Download and install <a href='http://www.partition-tool.com/download.htm'><b>EaseUS Partition Master Home Edition</b></a>.

<a href='http://www.partition-tool.com/easeus-partition-manager/linux-partition-manager.htm'><b>Here you can find</b></a> a detailed process with descriptions and screenshots.



### For MacOS Users ###


You can use <a href='http://code.google.com/p/macfuse'><b>MacFuse</b></a>.
Follow this <a href='http://code.google.com/p/macfuse/wiki/AUTOINSTALL'><b>guide</b></a> to install the program.



### Using the Router to Format the Disk Drive ###


Plug in your USB Disk and wait till USB indicator light to be on.  Once the light indicates that the drive has been mounted you may begin to work with the USB drive.

A briefly summary will be proceeded by details:

1) delete old partition table; <br />
2) create 'DOS' partition table; <br />
3) add a partition; <br />
4) format it with 'ext4'; <br />
5) commit all results. <br />


Open a terminal session, and connect to your router. You will be prompted for the password of the router. Enter the user's password. (the one you use to login to <a href='http://my.router'>webinterface</a>)

Once you are connected, you will see a BusyBox greeting and the prompt.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/term_greet.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/term_greet.png)

Before using the prompt to input commands, check to see if the disk is not mounted via the web interface.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/webiface1-en.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/webiface1-en.png)

With this example the disk is still mounted, and will need to be removed before proceeding. Press "Remove" within the Safely Remove Disk option to unmount the connected drive.


---

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **WARNING! DO NOT PROCEED IF THE DISK DRIVE IS STILL MOUNTED IN THE WEB INTERFACE!!**

---


![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/webiface2-en.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/webiface2-en.png)


To examine what partitions exist on the drive:

```
# cat /proc/partitions
major minor  #blocks  name

  31        0        192 mtdblock0
  31        1         64 mtdblock1
  31        2         64 mtdblock2
  31        3       1228 mtdblock3
  31        4       6579 mtdblock4
  31        5         64 mtdblock5
  31        6       7872 mtdblock6
   8        0    7910400 sda
   8        1    7908626 sda1
```

USB drives can be sda or sdb due to the possibility of connecting two USB drives to the RT-N56U USB ports. As you can see in the example here with one drive it is sda, and it has a single partition which is sda1.

```
# fdisk -lu /dev/sda

Disk /dev/sda: 8100 MB, 8100249600 bytes
175 heads, 12 sectors/track, 7533 cylinders, total 15820800 sectors
Units = sectors of 1 * 512 = 512 bytes

   Device Boot      Start         End      Blocks  Id System
/dev/sda1            2048    15819299     7908626  83 Linux
```

Create a new partition table and format it. Be careful you will need to perform the disk operations on volume (fdisk /dev/sda) not the partition (not fdisk /dev/sda1)!


#### If you don't need a swap partition ####
Create a new partition using "fdisk." (Input fdisk -u /dev/sda to work with sectors instead of cylinders)

```shell

#  fdisk /dev/sda

The number of cylinders for this disk is set to 7533.
There is nothing wrong with that, but this is larger than 1024,
and could in certain setups cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs
(e.g., DOS FDISK, OS/2 FDISK)

Command (m for help): m
Command Action
a       toggle a bootable flag
b       edit bsd disklabel
c       toggle the dos compatibility flag
d       delete a partition
l       list known partition types
n       add a new partition
o       create a new empty DOS partition table
p       print the partition table
q       quit without saving changes
s       create a new empty Sun disklabel
t       change a partition's system id
u       change display/entry units
v       verify the partition table
w       write table to disk and exit
x       extra functionality (experts only)

Command (m for help): d
Selected partition 1

Command (m for help): n
Command action
e   extended
p   primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-7533, default 1): Using default value 1
Last cylinder or +size or +sizeM or +sizeK (1-7533, default 7533): Using default value 7533

Command (m for help): p

Disk /dev/sda: 8100 MB, 8100249600 bytes
175 heads, 12 sectors/track, 7533 cylinders
Units = cylinders of 2100 * 512 = 1075200 bytes

Device Boot      Start         End      Blocks  Id System
/dev/sda1               1        7533     7908626  83 Linux

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table
```

Check the partition to see if it has been created.

```
# fdisk -lu /dev/sda

Disk /dev/sda: 8100 MB, 8100249600 bytes
175 heads, 12 sectors/track, 7533 cylinders, total 15820800 sectors
Units = sectors of 1 * 512 = 512 bytes

   Device Boot      Start         End      Blocks  Id System
/dev/sda1            2048    15819299     7908626  83 Linux
```


Now unmount the drive:
```
# ejusb
```

Now format the partition with volume label "Main". In the future, this partition will be mounted in the system with that label.

```
# mkfs.ext4 -m 0 -T largefile -L Main /dev/sda1
mke2fs 1.42.8 (20-Jun-2013)
Filesystem label=Main
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
7808 inodes, 1977156 blocks
0 blocks (0.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=2025848832
61 block groups
32768 blocks per group, 32768 fragments per group
128 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

Note: 5% of disk capacity is used by the super user don`t needs for system.

Either unplug disk, and plug in it again to create the following directories, or use these next 2 commands.

```
# mkdir /media/Main
# mount -t ext4 /dev/sda1 /media/Main
```


#### If you need a swap partition ####
You may need a SWAP partition if you intend to use applications like BitTorrent-clients or applications that require large amounts of memory (download managers, 'tiny servers', etc.). Also, **the presence of the SWAP partition is recommended when using a media server UPnP/DLNA**, which is in the process of database creation of media content consumed a large amount of RAM.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **Important note! It is not recommended to create swap files or partitions on USB hard drives. There is a risk of a system crash if the USB disk is unplugged incorrectly** (for example, if router is powered off suddenly, or some other reason).

```shell

# fdisk -u /dev/sda

Command (m for help): m
Command Action
a       toggle a bootable flag
b       edit bsd disklabel
c       toggle the dos compatibility flag
d       delete a partition
l       list known partition types
n       add a new partition
o       create a new empty DOS partition table
p       print the partition table
q       quit without saving changes
s       create a new empty Sun disklabel
t       change a partition's system id
u       change display/entry units
v       verify the partition table
w       write table to disk and exit
x       extra functionality (experts only)

Command (m for help): d
Selected partition 1

Command (m for help): n
Command action
e   extended
p   primary partition (1-4)
p
Partition number (1-4): 1
First sector (2048-15820799, default 2048): Using default value 2048
Last sector or +size or +sizeM or +sizeK (2048-15820799, default 15820799): +256M

Command (m for help): n
Command action
e   extended
p   primary partition (1-4)
p
Partition number (1-4): 2
First sector (502049-15820799, default 502049): Using default value 502049
Last sector or +size or +sizeM or +sizeK (502049-15820799, default 15820799): Using default value 15820799

Command (m for help): t
Partition number (1-4): 1
Hex code (type L to list codes): 82
Changed system type of partition 1 to 82 (Linux swap)

Command (m for help): p

Disk /dev/sda: 8100 MB, 8100249600 bytes
175 heads, 12 sectors/track, 7533 cylinders, total 15820800 sectors
Units = sectors of 1 * 512 = 512 bytes

Device Boot      Start         End      Blocks  Id System
/dev/sda1            2048      502048      250000+ 82 Linux swap
Partition 1 does not end on cylinder boundary
/dev/sda2          502049    15820799     7659375+ 83 Linux
Partition 2 does not end on cylinder boundary

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table
```


Now unmount the drive:
```
# ejusb
```

Now format the partition with volume label "Main".
```
# mkfs.ext4 -m 0 -T largefile -L Main /dev/sda2
mke2fs 1.42.8 (20-Jun-2013)
Filesystem label=Main
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
7552 inodes, 1914843 blocks
0 blocks (0.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=1962934272
59 block groups
32768 blocks per group, 32768 fragments per group
128 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

And create the swap space:
```
# mkswap /dev/sda1
Setting up swapspace version 1, size = 255996416 bytes
```

The swap partition will be mounted automatically on boot or when you plug-in USB disk.


## Using Entware ##

If the USB drive has not been plugged in, go ahead and do so now.  Open a terminal (PuTTY), and log into the RT-N56U.  Next step is to create a new directory.


Check to see if the disk was mounted via the terminal.

```
# mount
rootfs on / type rootfs (rw)
/dev/root on / type squashfs (ro,relatime)
proc on /proc type proc (rw,relatime)
sysfs on /sys type sysfs (rw,relatime)
usbfs on /proc/bus/usb type usbfs (rw,relatime)
tmpfs on /dev type tmpfs (rw,relatime,size=8k)
tmpfs on /etc type tmpfs (rw,noatime,size=2048k)
tmpfs on /home type tmpfs (rw,relatime,size=1024k)
tmpfs on /media type tmpfs (rw,relatime,size=8k)
tmpfs on /mnt type tmpfs (rw,relatime,size=8k)
tmpfs on /tmp type tmpfs (rw,relatime,size=24576k)
tmpfs on /var type tmpfs (rw,relatime,size=4096k)
devpts on /dev/pts type devpts (rw,relatime,mode=600)
/dev/sda1 on /media/Main type ext4 (rw,noatime,data=ordered)
```

Now to create the new directory

```
# mkdir /media/Main/opt
```

Now, unmount the disk drive:
```
# ejusb
```

Go to <a href='http://my.router/Advanced_AiDisk_others.asp'><b>Advanced setting -> USB Application -> Common setting</b></a> of router's web interface. Switch "Allow Run Optware" to "Entware" and then finally press "Apply" to save the setting.


![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/webiface3-en.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/webiface3-en.png)

Unplug the USB drive, and then plug it in again. Wait for the USB indicator light to indicate it is ready to use the drive on the router,  and then use the "mount" command in the terminal to check the output of the drive.

```
# mount
rootfs on / type rootfs (rw)
/dev/root on / type squashfs (ro,relatime)
proc on /proc type proc (rw,relatime)
sysfs on /sys type sysfs (rw,relatime)
usbfs on /proc/bus/usb type usbfs (rw,relatime)
tmpfs on /dev type tmpfs (rw,relatime,size=8k)
tmpfs on /etc type tmpfs (rw,noatime,size=2048k)
tmpfs on /home type tmpfs (rw,relatime,size=1024k)
tmpfs on /media type tmpfs (rw,relatime,size=8k)
tmpfs on /mnt type tmpfs (rw,relatime,size=8k)
tmpfs on /tmp type tmpfs (rw,relatime,size=24576k)
tmpfs on /var type tmpfs (rw,relatime,size=4096k)
devpts on /dev/pts type devpts (rw,relatime,mode=600)
/dev/sda1 on /media/Main type ext4 (rw,noatime,data=ordered)
/dev/sda1 on /opt type ext4 (rw,noatime,data=ordered)
```

As you can see the partition /dev/sda1 mounted to /media/Main and the next line shows that /media/Main/opt is mounted to /opt.

Again, if you have swap partition /dev/sda1 you'll see another output:
```
# mount
rootfs on / type rootfs (rw)
/dev/root on / type squashfs (ro,relatime)
proc on /proc type proc (rw,relatime)
sysfs on /sys type sysfs (rw,relatime)
usbfs on /proc/bus/usb type usbfs (rw,relatime)
tmpfs on /dev type tmpfs (rw,relatime,size=8k)
tmpfs on /etc type tmpfs (rw,noatime,size=2048k)
tmpfs on /home type tmpfs (rw,relatime,size=1024k)
tmpfs on /media type tmpfs (rw,relatime,size=8k)
tmpfs on /mnt type tmpfs (rw,relatime,size=8k)
tmpfs on /tmp type tmpfs (rw,relatime,size=24576k)
tmpfs on /var type tmpfs (rw,relatime,size=4096k)
devpts on /dev/pts type devpts (rw,relatime,mode=600)
/dev/sda2 on /media/Main type ext4 (rw,noatime,data=ordered)
/dev/sda2 on /opt type ext4 (rw,noatime,data=ordered)
```



---

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **WARNING! NEVER UNPLUG YOUR DISK UNTIL IT HAS BEEN REMOVED SAFELY, OR HAS BEEN UNMOUNTED VIA THE TERMINAL!**

---



## Install Applications How To ##

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **ATTENTION! Before installing any apps strongly recommended to update the information about the repository!**:
```
# opkg update
# opkg upgrade
```

---


To install an application from the Entware repository use:

```
# opkg install { app_name }
```

This command installs application with its dependencies.


---

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **NOTE: Never remove anything by yourself from /opt directory on your disk. Use:**
```
# opkg remove { app_name }
```


---

For example if you need a Midnight Commander, use:

```
# opkg update
# opkg install mc
```

This will install Midnight Commander.


---

Use **opkg list** to see the whole list of applications avaliable in repository.<br>
To get more info use <b>opkg --help</b>.<br>
<br>
<hr />
<b>Entware has a Search by names and descriptions of packages:</b>
<pre><code># opkg find "*game*"<br>
</code></pre>
<hr />

<h2>Install xUpnpd</h2>
<pre><code># opkg update<br>
# opkg install xupnpd<br>
</code></pre>

Launching xUpnpd:<br>
<pre><code># /opt/etc/init.d/S94xupnpd start <br>
</code></pre>

After install xUpnpd you may edit configuration of it in directory /opt/share/xupnpd (Can be edited by <a href='http://my.router:4044'>WEB-interface</a>)..<br>
<hr />
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png' />  <b>NOTE: All configuration files of any Apps must be saved as UNIX-Style!!!</b> <br>
For example, you may install Midnight Commander and edit all configuration files from it.<br>
<hr />


If you'd like some application start on boot check the first letter of script, which invokes it in /opt/etc/init.d. It should be 'S'.<br>
<br>
<pre><code>#  ls -a /opt/etc/init.d<br>
.            ..           S01system    S10iptables  S94xupnpd    rc.func      rc.unslung<br>
</code></pre>

<hr />
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png' />  <b>IMPORTANT!! When you install any application ALWAYS check what it can be completely stopped with script in /opt/etc/init.d</b><br>
If it doesn't stop your information on disk (e.g. file-system) may be seriously damaged!<b><br>
<hr /></b>


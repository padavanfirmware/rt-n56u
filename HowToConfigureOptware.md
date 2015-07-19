

# How To Configure Router For Optware Usage With 1.0.1.7f-p4 Or Later Released Versions Of The Firmware #

---



<a href='http://en.wikipedia.org/wiki/Optware'>Optware</a> is an advanced package manager which allows you to easily install, and uninstall cross-compiled Linux applications to your device over the internet. At this time, Optware supports the automatic download and installation of via 1500 programs.


## Installation and Usage of the Terminal Application ##


First, open your browser, select in the lower left pane <a href='http://my.router/Advanced_System_Content.asp'>Advanced Setting -> Administration -> System</a>
and choose a server you'd like to use. Note, that it is highly recommended to use SSH as the server for external connections only.  Because Telnet is an insecure protocol, and is the very replacement for it.  However, for private (internal) network usage security may not be a necessity.

![http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/adm-system.png](http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/adm-system.png)

In the above example SSH has been selected as the preferred method.  Select the option that you wish to use and then apply to save the settings to the router.

You'll need a <a href='http://en.wikipedia.org/wiki/Terminal_emulator'>terminal client</a> to establish a connection with RT-N56U. The terminal application is a serial computer interface for text entry and display output. There are many different applications. You should choose one by your OS.



### Directions for Windows XP, Vista, and Windows 7 users ###


<a href='http://www.putty.org/'><b>PuTTY</b></a>. is a free implementation of Telnet and SSH for Windows and Unix. Download the installer, and install the application.  After installation there is minimal configuration needed to access the router.  To start the session, you will need to enter a few basic parameters. Within the "Session" category select  "Host Name" field, enter _**my.router**_ or _**the IP address of router**_. Select a login protocol to use, from the "Connection type" that matches the protocol configured for the router.  Afterwards, select the Translation category and make sure that UTF-8 is configured for the character set field.

![http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/putty_932x448.png](http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/putty_932x448.png)



---

**IMPORTANT NOTE: NEVER SAVE YOUR LOGIN AND / OR PASSWORD TO ANY CLIENT WHEN YOU USE TERMINAL CONNECTION!!**

---



Once you have finished the proper configurations, select the "Open" button at the bottom right of the configuration window, and PuTTY will initiate the connection to the router using the proper protocol.


### Directions for MacOS Users ###

<table>
<tr>
<td width='400'>
Open Finder, and go to Applications => Utilities. Double click on Terminal, or highlight Terminal and Apple/Command Key + Arrow Down.<br>
</td>
<td>
<img src='http://rt-n56u.googlecode.com/svn/pic/terminal_in_osx.jpg' />
</td>
</tr>
</table>

```
ssh admin@my.router
```

or use one of the alias names: ```
ssh admin@rt-n56u, ssh admin@my.rt-n56u```


## USB Disk Formatting ##


Linux based systems use [EXTended filesystem](http://en.wikipedia.org/wiki/Extended_file_system). It is recommended to use an external disk (HDD, Flash) that is more than 512MB in  capacity, and is formatted with EXT2 or EXT3 filesystem.

**NOTE: _It is not recommended to use a USB disk that has a larger  than 2TB capacity to avoid driver, and possible data issues. It is possible, but not recommended to use NTFS disks on Linux.  The instructions will be based on the recommended Linux filesystem_**.



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
4) format it with 'ext3'; <br />
5) commit all results. <br />


Open a terminal session, and connect to your router. You will be prompted for the password of the router. Enter the user's password. (the one you use to login to <a href='http://my.router'>webinterface</a>)

Once you are connected, you will see a BusyBox greeting and the prompt.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/term_greet.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/term_greet.png)

Before using the prompt to input commands, check to see if the disk is not mounted via the web interface.

![http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/webiface1.png](http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/webiface1.png)

With this example the disk is still mounted, and will need to be removed before proceeding. Press "Remove" within the Safely Remove Disk option to unmount the connected drive.


---

**WARNING! DO NOT PROCEED IF THE DISK DRIVE IS STILL MOUNTED IN THE WEB INTERFACE!!**

---


![http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/webiface2.png](http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/webiface2.png)


To examine what partitions exist on the drive:

```
# cat /proc/partitions

major minor  #blocks  name

  31     0        192 mtdblock0
  31     1         64 mtdblock1
  31     2         64 mtdblock2
  31     3       7872 mtdblock3
   8     0    7823360 sda
   8     1    7816773 sda1
```

USB drives can be sda or sdb due to the possibility of connecting two USB drives to the RT-N56U USB ports. As you can see in the example here with one drive it is sda, and it has a single partition which is sda1.

```
# fdisk -l /dev/sda

Disk /dev/sda: 8011 MB, 8011120640 bytes
247 heads, 62 sectors/track, 1021 cylinders
Units = cylinders of 15314 * 512 = 7840768 bytes

   Device Boot      Start         End      Blocks  Id System
/dev/sda1               1        1021     7816773  83 Linux
```

Create a new partition table and format it. Be careful you will need to perform the disk operations on volume (fdisk /dev/sda) not the partition (not fdisk /dev/sda1)!


#### If you don't need a swap partition ####
Create a new partition using "fdisk." (Input fdisk -u /dev/sda to work with sectors instead of cylinders)

```shell

# fdisk /dev/sda

Command (m for help): m
Command Action
a	toggle a bootable flag
b	edit bsd disklabel
c	toggle the dos compatibility flag
d	delete a partition
l	list known partition types
n	add a new partition
o	create a new empty DOS partition table
p	print the partition table
q	quit without saving changes
s	create a new empty Sun disklabel
t	change a partition's system id
u	change display/entry units
v	verify the partition table
w	write table to disk and exit
x	extra functionality (experts only)

Command (m for help): d
Selected partition 1

Command (m for help): o
Building a new DOS disklabel. Changes will remain in memory only,
until you decide to write them. After that the previous content
won't be recoverable.


Command (m for help): n
Command action
e   extended
p   primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-1021, default 1): Using default value 1
Last cylinder or +size or +sizeM or +sizeK (1-1021, default 1021): Using default value 1021

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table
```

Check the partition to see if it has been created.

```
# fdisk -l /dev/sda

Disk /dev/sda: 8011 MB, 8011120640 bytes
247 heads, 62 sectors/track, 1021 cylinders
Units = cylinders of 15314 * 512 = 7840768 bytes

   Device Boot      Start         End      Blocks  Id System
/dev/sda1               1        1021     7816773  83 Linux
```


After partitioning of the drive the system may mount the disk automatically for you. If it does, you will need to remove the drive safely once more via the web interface as done in the previously example to remove the drive safely.
(go to http://my.router/ and press 'Remove')

Now format the partition.

```
# mke2fs -t ext3 -b 4096 /dev/sda1
mke2fs 1.41.12 (17-May-2010)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
488640 inodes, 1954193 blocks
97709 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=2004877312
60 block groups
32768 blocks per group, 32768 fragments per group
8144 inodes per group
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Writing inode tables: done                            
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 36 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
```

Note: 5% of disk capacity is used by the super user for system needs.

Either unplug disk, and plug in it again to create the following directories, or use these next 2 commands.

```
# mkdir /media/AiDisk_a1
# mount -t ext3 /dev/sda1 /media/AiDisk_a1
```


#### If you need a swap partition ####
You may need swap partition with the more recent firmwares.  If you'd like to use such applications as BitTorrent clients or applications which require much of the system memory (downloaders, 'tiny servers', etc).
**Important note! It is not recommended to create swap files or partitions on USB hard drives. There is a risk of a system crash if the USB disk is unplugged incorrectly** (for example, if router is powered off suddenly, or some other reason).

```shell

# fdisk /dev/sda

Command (m for help): m
Command Action
a	toggle a bootable flag
b	edit bsd disklabel
c	toggle the dos compatibility flag
d	delete a partition
l	list known partition types
n	add a new partition
o	create a new empty DOS partition table
p	print the partition table
q	quit without saving changes
s	create a new empty Sun disklabel
t	change a partition's system id
u	change display/entry units
v	verify the partition table
w	write table to disk and exit
x	extra functionality (experts only)

Command (m for help): o
Building a new DOS disklabel. Changes will remain in memory only,
until you decide to write them. After that the previous content
won't be recoverable.


Command (m for help): p

Disk /dev/sda: 8011 MB, 8011120640 bytes
247 heads, 62 sectors/track, 1021 cylinders
Units = cylinders of 15314 * 512 = 7840768 bytes

Device Boot      Start         End      Blocks  Id System

Command (m for help): n
Command action
e   extended
p   primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-1021, default 1): Using default value 1
Last cylinder or +size or +sizeM or +sizeK (1-1021, default 1021): +256M

Command (m for help): n
Command action
e   extended
p   primary partition (1-4)
p
Partition number (1-4): 2
First cylinder (35-1021, default 35): Using default value 35
Last cylinder or +size or +sizeM or +sizeK (35-1021, default 1021): Using default value 1021

Command (m for help): t
Partition number (1-4): 1
Hex code (type L to list codes): 82
Changed system type of partition 1 to 82 (Linux swap)

Command (m for help): p

Disk /dev/sda: 8011 MB, 8011120640 bytes
247 heads, 62 sectors/track, 1021 cylinders
Units = cylinders of 15314 * 512 = 7840768 bytes

Device Boot      Start         End      Blocks  Id System
/dev/sda1               1          34      259314  82 Linux swap
/dev/sda2              35        1021     7557459  83 Linux

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table
```

Now format the partition.

```
# mke2fs -t ext3 -b 4096 /dev/sda2
mke2fs 1.41.12 (17-May-2010)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
488640 inodes, 1954193 blocks
97709 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=2004877312
60 block groups
32768 blocks per group, 32768 fragments per group
8144 inodes per group
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Writing inode tables: done                            
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 36 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
```

And create the swap space:
```
# mkswap /dev/sda1
Setting up swapspace version 1, size = 265533440 bytes
```

The swap partition will be mounted automatically on boot or when you plug-in USB disk.


## Using Optware ##

If the USB drive has not been plugged in, go ahead and do so now.  Open a terminal (PuTTY), and log into the RT-N56U.  Next step is to create a new directory.


Check to see if the disk was mounted via the terminal.

```
# mount
rootfs on / type rootfs (rw)
none on /proc type proc (rw)
none on /var type ramfs (rw)
none on /etc type ramfs (rw)
none on /tmp type ramfs (rw)
none on /media type ramfs (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw)
mdev on /dev type ramfs (rw)
devpts on /dev/pts type devpts (rw)
none on /proc/bus/usb type usbfs (rw)
nfsd on /proc/fs/nfsd type nfsd (rw)
/dev/sda1 on /media/AiDisk_a1 type ext3 (rw,data=ordered)
```

Now to create the new directory

```
# mkdir /media/AiDisk_a1/opt
```

Now, unmount the disk drive:
```
# umount /media/AiDisk_a1
# rm -rf /media/AiDisk_a1
```

**Note: if you've set swap partition to /dev/sda1, you your disk will be /media/AiDisk\_a2. So, you should do:**

```
# mkdir /media/AiDisk_a2/opt
```

Now, unmount the disk drive:
```
# umount /media/AiDisk_a2
# rm -rf /media/AiDisk_a2
```

Go to <a href='http://my.router/Advanced_AiDisk_others.asp'><b>Advanced setting -> USB Application -> Miscellaneous setting</b></a> of router's web interface. Switch "Allow Run Optware" to "Yes" and then finally press "Apply" to save the setting.


![http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/webiface3.png](http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/webiface3.png)

Unplug the USB drive, and then plug it in again. Wait for the USB indicator light to indicate it is ready to use the drive on the router,  and then use the "mount" command in the terminal to check the output of the drive.

```
# mount
rootfs on / type rootfs (rw)
none on /proc type proc (rw)
none on /var type ramfs (rw)
none on /etc type ramfs (rw)
none on /tmp type ramfs (rw)
none on /media type ramfs (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw)
mdev on /dev type ramfs (rw)
devpts on /dev/pts type devpts (rw)
none on /proc/bus/usb type usbfs (rw)
nfsd on /proc/fs/nfsd type nfsd (rw)
/dev/sda1 on /media/AiDisk_a1 type ext3 (rw,noatime,data=ordered)
/dev/sda1 on /opt type ext3 (rw,noatime,data=ordered)
rpc_pipefs on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
```

As you can see the partition /dev/sda1 mounted to /media/AiDIsk\_a1 and the next line shows that /media/AiDIsk\_a1/opt is mounted to /opt.

Again, if you have swap partition /dev/sda1 you'll see another output:
```
# mount
...
/dev/sda2 on /media/AiDisk_a2 type ext3 (rw,noatime,data=ordered)
/dev/sda2 on /opt type ext3 (rw,noatime,data=ordered)
...
```



---

**WARNING! NEVER UNPLUG YOUR DISK UNTIL IT HAS BEEN REMOVED SAFELY, OR HAS BEEN UNMOUNTED VIA THE TERMINAL!**

---


You can observe information about CPU usage by using the following command:

```
# cpu
CPU:  busy 0%  (system=0% user=0% nice=0% idle=100%)

or avarage

# cpu -a
CPU:  average 0%  (system=0% user=0% nice=0% idle=99%)
```


## Install Applications How To ##

To install an application from the optware repository use:

```
# ipkg install { app_name }
```

This command installs application with its dependencies.


---

**NOTE: Never remove anything by yourself from /opt directory on your disk. Use:**

---


```
# ipkg remove { app_name }
```


For example if you need a torrent client, use:

```
# ipkg install transmission
Installing transmission (2.42-1) to /opt/...
Downloading http://ipkg.nslu2-linux.org/feeds/optware/oleg/cross/stable/transmission_2.42-1_mipsel.ipk
Installing openssl (0.9.7m-5) to /opt/...
Downloading http://ipkg.nslu2-linux.org/feeds/optware/oleg/cross/stable/openssl_0.9.7m-5_mipsel.ipk
Installing libcurl (7.21.7-1) to /opt/...
Downloading http://ipkg.nslu2-linux.org/feeds/optware/oleg/cross/stable/libcurl_7.21.7-1_mipsel.ipk
Installing zlib (1.2.5-1) to /opt/...
Downloading http://ipkg.nslu2-linux.org/feeds/optware/oleg/cross/stable/zlib_1.2.5-1_mipsel.ipk
Installing libevent (2.0.11-1) to /opt/...
Downloading http://ipkg.nslu2-linux.org/feeds/optware/oleg/cross/stable/libevent_2.0.11-1_mipsel.ipk
Configuring libcurl
Configuring libevent
Configuring openssl
Configuring transmission
Configuring zlib
Successfully terminated.
```

This will install torrent client with web interface control.

Use **ipkg list** to see the whole list of applications avaliable in repository.
To get more info use **ipkg --help**.

If you'd like some application start on boot check the first letter of script, which invokes it in /opt/etc/init.d. It should be 'S'.

```
# ls -a /opt/etc/init.d 
.                ..               K01system        K95aria2         K95transmission  S10iptables
```

This means that Transmission will not start on boot.
To change it use:

```
# mv /opt/etc/init.d/K95transmission /opt/etc/init.d/S95transmission 


# ls -a /opt/etc/init.d
.                ..               K01system        K95aria2         S10iptables      S95transmission
```

---

**IMPORTANT!! When you install any application ALWAYS check it can be completely stopped with script in /opt/etc/init.d**<br>
If it doesn't stop your disk can be seriously damaged!<b><br>
<hr /></b>

Let's do one more step (optional, if you didn't change the IP address of your router).<br>
I'd like to show you how to edit configuration files.<br>
First we need to start and then stop transmission daemon.<br>
<br>
<pre><code># /opt/etc/init.d/S95transmission start<br>
<br>
# /opt/etc/init.d/S95transmission stop<br>
</code></pre>

After that transmission configuration path should be created.<br>
<br>
If you really do need to change only one parameter 'umask' and don't want to install anything use the following command:<br>
<br>
<pre><code># sed -i 's/\"umask\"\:.*$/\"umask\"\:\ 0\,/' "/opt/etc/transmission-daemon/settings.json"<br>
</code></pre>

But if you want to use interactive editor, there is built-in one called <a href='http://en.wikipedia.org/wiki/Vi'><b>VI</b></a>. It's a little bit difficult to use it if you haven't used Linux before.<br>
You can read more about <a href='http://www.washington.edu/computing/unix/vi.html'>VI here</a>.<br>
<br>
But there some alternatives in the optware repository, which are much user-friendly.<br>
For example, nano.<br>
<br>
<pre><code># ipkg install nano<br>
</code></pre>

<pre><code># nano /opt/etc/transmission-daemon/settings.json<br>
</code></pre>

Find the next line:<br>
<pre><code>...<br>
"umask": 18,<br>
...<br>
</code></pre>

And change '18' to 0:<br>
<pre><code>...<br>
"umask": 0,<br>
...<br>
</code></pre>

<b>Press CTRL+O</b> to write changes to file. Then <i><b>nano</b></i> will ask what file to write these changes - <b>Press Enter</b>.<br>
<b>Press CTRL+X</b> to exit interactive editor.<br>
<br>
<br>
<a href='https://trac.transmissionbt.com/wiki/ConfigurationParameters'><b>Here you can read</b></a> about all transmission configuration parameters.<br>
<br>
Then close terminal session (type exit) and reboot your router using webinterface.<br>
<br>
Goto your web browser and follow:<br>
<pre><code>http://my.router:9091<br>
</code></pre>

<i>Note: You are able to use <a href='http://my.router'>http://my.router</a> only in home network!</i>


<h3>Remote access</h3>

There is a possibility to manage your downloads from internet.<br>
<br>
First, you need to enable UPnP in your web panel <a href='http://my.router/Advanced_WAN_Content.asp'><b>Advanced setting -> WAN -> Internet Connection</b></a>.<br>
<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/upnp.png' />

Then you need to add 1 rule to iptables, go to <a href='http://my.router/Advanced_VirtualServer_Content.asp'><b>Advanced setting -> WAN -> Virtual server</b></a>

and add:<br>
<br>
<pre><code>tsmd		9091		192.168.1.1		9091		TCP<br>
</code></pre>


Now, you possibly want to use login form on this page.<br>
<br>
Make sure Transmission is not working now:<br>
<pre><code># /opt/etc/init.d/S95transmission stop<br>
</code></pre>

Update your starting script:<br>
<pre><code># echo '' &gt; /opt/etc/init.d/S95transmission<br>
# wget -c -O /opt/etc/init.d/S95transmission http://dl.dropboxusercontent.com/u/44733876/googlecode/share/S95transmission<br>
</code></pre>

Edit starting script, find the lines below and replace values with your login data:<br>
<pre><code># nano /opt/etc/init.d/S95transmission<br>
<br>
...<br>
	######################################<br>
	LOGIN="your_login_here"<br>
	MYSECRET="YoUr_SeCrEt"<br>
	######################################<br>
...<br>
<br>
</code></pre>


If you don't want to use remote access, then comment the rules with '#':<br>
<pre><code>#!/bin/sh<br>
<br>
<br>
case "$1" in<br>
start|update)<br>
        # add iptables custom rules<br>
        echo "firewall started"<br>
  #	iptables -I INPUT -p tcp --destination-port 9091 -j ACCEPT<br>
	exit 0<br>
        ;;<br>
stop)<br>
        # delete iptables custom rules<br>
  #	iptables -D INPUT -p tcp --destination-port 9091 -j ACCEPT<br>
        echo "firewall stopped"<br>
	exit 0<br>
        ;;<br>
*)<br>
	echo "Usage: $0 {start|stop|update}"<br>
        exit 1<br>
        ;;<br>
esac<br>
</code></pre>

and run:<br>
<pre><code># /opt/etc/init.d/S10iptables update<br>
</code></pre>

And comment with '#' login and password as well:<br>
<pre><code># nano /opt/etc/init.d/S95transmission<br>
<br>
...<br>
	######################################<br>
  #	LOGIN="your_login_here"<br>
  #	MYSECRET="YoUr_SeCrEt"<br>
	######################################<br>
...<br>
<br>
</code></pre>
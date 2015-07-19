

# Common Tips #
Useful small tips and recipes are being posted here.
Most of these tips are based on external applications. See <a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureEntware'><b>instructions for setting up Entware</b></a> first.

---



## The features of firmware from Padavan. ##

  * All firmwares can be downloaded <a href='https://drive.google.com/folderview?id=0B0clSzFg6jb9ejVLX0cyR0ZpMWs&usp=sharing#list'>here</a>.
  * You able to <a href='http://code.google.com/p/rt-n56u/wiki/HowToMakeFirmware'>create a custom firmware</a> with the necessary parameters.
  * After upgrading from the factory firmware, all settings of the router will be reset automatically.
  * Do not load the configuration file from the factory firmware.
  * WAN MAC address may be different from that on the label by 2 bits in the last octet (useful for model RT-N14U). If your ISP uses to authenticate bind to MAC-address, set the MAC from labels at <a href='http://my.router/Advanced_WAN_Content.asp'>WAN settings</a>. Or call to the provider's admin to rebind MAC.
  * If something does not work right, look primarily at <a href='http://my.router/Main_LogStatus_Content.asp'>system log</a>.
  * To conserve flash memory router has a manual mode to save the configuration (<a href='http://my.router/Advanced_SettingBackup_Content.asp'>Administration -> Settings</a>); when it is turned in the top panel a button "Save" will appear.
  * For providers offering PPPoE-connection + IPTV, you must enable PPPoE VPN + MAN: ZeroConf in the <a href='http://my.router/Advanced_WAN_Content.asp'>WAN settings</a>.
  * For ease of mount a USB-drive, it is better to create a volume label in Latin. In this case, the drive will always be mounted under a single name.
  * <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips#How_to_configure_built-in_Transmission'>Transmission</a> and Aria2 before the first start require the creation of a directory in the root of the drive, see the tooltip. Why it is so and not otherwise, youwill understand when you will use different drives.
  * <a href='http://code.google.com/p/transmisson-remote-gui/'>Transmission Remote GUI</a> is the most convenient client for the  Transmission.
  * The best filesystem for downloads - EXT4. The firmware has all the tools to work with it.
  * Do not download the torrents to Flash-drives.
  * The router has a limited amount of RAM; the most demanding applications is transmission, minidlna, aria2; whenever possible, do not run them simultaneously.
  * Offload UDP through HW\_NAT is disabled by default, so uTP and UDP traffic in uTorrent (and other torrent clients) can greatly load CPU. The best option - disable uTP in torrent client, then all TCP traffic will offload, while at speeds of 10-11 MB / sec CPU usage is almost zero. The second option - enable UDP offload, but it does have some limitations.


The firmware "base" does not include the USB applications:
  * DLNA media server minidlna
  * Torrent client transmission
  * Download manager aria2
  * iTunes media server firefly
All of these, as well as most other applications <a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureEntware'>can be installed from the Entware-repository</a> into the USB drive.

---



## What is difference between the versions (full, base, etc.) of Firmware? ##

This firmware exists for routers Asus RT-N56U/RT-N65U/RT-N14U. There are also several Firmware builds (full, base, etc.). You can read about the differences <a href='http://code.google.com/p/rt-n56u/wiki/FirmwareBuilds'>in this section</a>.

---



## Where can I see list of changes in last version of Firmware? ##

All important changes in Firmware are published in <a href='http://rt-n56u.googlecode.com/git/changes.eng.txt'>this file</a>.

Full information about changes to Firmware you can see <a href='https://code.google.com/p/rt-n56u/source/list'>at this page</a>.

---



## Installation and Usage the Terminal Application ##

First, open your browser, select in the lower left pane <a href='http://my.router/Advanced_System_Content.asp'>Advanced Settings -> Administration -> System</a>
and choose a server you'd like to use. Note, that it is highly recommended to use SSH as the server for external connections only.  Because Telnet is an insecure protocol, and is the very replacement for it.  However, for private (internal) network usage security may not be a necessity.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/adm-system-en.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/adm-system-en.png)

In the above example SSH has been selected as the preferred method. Select the option that you wish to use and then apply to save the settings to the router.

You'll need a <a href='http://en.wikipedia.org/wiki/Terminal_emulator'>terminal client</a> to establish a connection with RT-N56U. The terminal application is a serial computer interface for text entry and display output. There are many different applications. You should choose one by your OS.



### Directions for Windows XP, Vista, and Windows 7 users ###

<a href='http://www.putty.org/'><b>PuTTY</b></a> is a free implementation of Telnet and SSH for Windows and Unix. Download the installer, and install the application.  After installation there is minimal configuration needed to access the router.  To start the session, you will need to enter a few basic parameters. Within the "Session" category select  "Host Name" field, enter _**my.router**_ or _**the IP address of router**_. Select a login protocol to use, from the "Connection type" that matches the protocol configured for the router.  Afterwards, select the Translation category and make sure that UTF-8 is configured for the character set field.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/putty_932x448.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/putty_932x448.png)


![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **IMPORTANT NOTE: NEVER SAVE YOUR LOGIN AND / OR PASSWORD TO ANY CLIENT WHEN YOU USE TERMINAL CONNECTION!!!**


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

---



## How do I edit the scripts/configuration files? ##
1. Built-in utility **vi**.
Run command
```
# vi your_file
```
.
Point the cursor on any blank line.
Press the "i" on the keyboard.
Insert the desired construction to the text. If necessary, use the button ENTER.
When finished, press the keyboard "Esc", then type ":wq" (without the quotes) and press ENTER.
Additional information about vi can be found in Google.

2. More convenient / more evident to use the editor built into the Midnight Commander.
To install the Midnight Commander, run the command:
```
# opkg update
# opkg install mc
```
To start the Midnight Commander`s Editor connect to the router via Telnet/SSH console and run the command:
```
# mcedit your_file
```

---



## Using a script to load information about ISP`s static routes ##
1. <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips#How_do_I_edit_the_scripts/configuration_files?'>Edit</a> the file /etc/storage/post\_wan\_script.sh and add to it all lines with routes in the following format:
```
ip route add xxx.xxx.xxx.xxx/yy via zzz.zzz.zzz.zzz
```
where xxx.xxx.xxx.xxx - IP-lan, yy - mask in CIDR-format, and zzz.zzz.zzz.zzz - gateway.
Save file.

2. Run in console
```
# mtd_storage.sh save
```

3. Restart PPTP-session and check that the routes is loaded. To do this, run the command **route** in the console.

---



## What are the existing network interfaces (transcript naming interfaces)? ##
  * br0 = LAN + WLAN + AP-Client + WDS
  * eth2 = Ethernet interface GMAC1, that connected to the switch (trunk port).
  * eth2.1 = LAN (VLAN VID1)
  * eth2.2 = WAN (VLAN VID2)
  * ra0 = WLAN 5GHz
  * ra1 = WLAN 5GHz Guest
  * rai0 = WLAN 2.4GHz
  * rai1 = WLAN 2.4GHz Guest
  * apcli0 = AP-Client 5GHz
  * apclii0 = AP-Client 2.4GHz
  * wds0-wds3 = WDS 5GHz
  * wdsi0-wdsi3 = WDS 2.4GHz

In the no-VLAN firmware
  * eth2 = LAN
  * eth3 = WAN

---



## Using the built-in scheduler (crond) ##
![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png) **Warming!** Use the example of code below for firmware version _3.x.3.8-086_ or less.

1. Create file with cron tasks:
```
touch /etc/storage/cron
```

2. Add the following code to /etc/storage/started\_script.sh:
```
############################# user crontabs create #############################
fix_crond_env() {
 local CRON_USER=`nvram get http_username 2>/dev/null`
 if [ -n "$CRON_USER" ] ; then
   mkdir -p -m 700 /var/spool/cron/crontabs
   ln -s /etc/storage/cron /var/spool/cron/crontabs/$CRON_USER
   [ -z "`pidof crond`" ] && /usr/sbin/crond
 fi
}
fix_crond_env
################################################################################
```


---

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png) Starting from firmware version _3.x.3.8-087_ add the following lines to /etc/storage/started\_script.sh:
```
### Start cron daemon
[ -z "`pidof crond`" ] && /usr/sbin/crond
```

---


3. Create test script
```
mkdir /etc/storage/cron.d
```

Add the following code to /etc/storage/cron.d/example.sh and add this text to it:
```
#!/bin/bash
case "$1" in
 old) logger -t "$0" "Good bye old year" ;;
 new) logger -t "$0" "Happy new year"    ;;
 *)   
   DAYS=$((1 + (`date -d $(date +%Y)-12-31 +%s` - `date +%s`)/86400))
   logger -t "$0" "$DAYS days to new year"
   ;;
esac
```

4. Give permission to run the script /etc/storage/cron.d/example.sh
```
chmod 700 /etc/storage/cron.d/example.sh
```

5. Run in console:
```
# /etc/storage/started_script.sh
```

6. Now let's add tasks to the scheduler
To edit cron jobs use:
```
crontab -e
```

And add the following:
```
SHELL=/bin/sh
MAILTO=root
HOME=/
59 23 31 12 * /etc/storage/cron.d/example.sh old
01 00 01 01 * /etc/storage/cron.d/example.sh new
30 07  *  * * /etc/storage/cron.d/example.sh
```

To list cron jobs use:
```
crontab -l
```

7. Do not forget to execute after modifications:
```
mtd_storage.sh save
```

The new crontab will be created for user with uid = 0 every time the router boots.
In the example above at 23:59 on December 31 you will see "Good bye old year", and at 00:01 on January 1 "Happy new year" in syslog. Also it will write to syslog days remaining to the new year every day at 7:30.

---



## How to turn on a computer on the local network using the Wake-on-LAN ##
> Wake-on-LAN (WOL) is an Ethernet computer networking standard that allows a computer to be turned on or awakened by a network message. Equivalent terms include wake on WAN, remote wake-up, power on by LAN, power up by LAN, resume by LAN, resume on LAN and wake up on LAN. In case the computer being woken is communicating via Wi-Fi, a supplementary standard called Wake on Wireless LAN (WoWLAN) must be employed.

> Wake-on-LAN ("WOL") is implemented using a specially designed packet called a magic packet, which is sent to the computer to be woken up. The magic packet contains the MAC address of the destination computer, an identifying number built into each network interface card ("NIC") or other ethernet device in a computer, that enables it to be uniquely recognized and addressed on a network. Powered-down or turned off computers capable of Wake-on-LAN will contain network devices able to "listen" to incoming packets in low-power mode while the system is powered down. If a magic packet is received that is directed to the device's MAC address, the NIC signals the computer's power supply or motherboard to initiate system wake-up, much in the same way as pressing the power button would do.

### Hardware requirements for Wake-on-LAN ###
Wake-on-LAN support is implemented on the motherboard of a computer and the network interface (firmware), and is consequently not dependent on the operating system running on the hardware. Some operating systems can control Wake-on-LAN behaviour via NIC drivers. If the network interface is a plug-in card rather than being integrated into the motherboard, the card may need to be connected to the motherboard by an additional cable. Motherboards with an embedded Ethernet controller which supports Wake-on-LAN do not need a cable. The power supply must meet ATX 2.01 specifications.
Wake-on-LAN usually needs to be enabled in the Power Management section of a PC motherboard's BIOS setup utility, although on some systems, such as Apple computers, it is enabled by default. On older systems the bios setting may be referred to as "WOL", on newer systems supporting PCI version 2.2, it may be referred to as "PME" (Power Management Events, which include WOL). It may also be necessary to configure the computer to reserve standby power for the network card when the system is shut down.

### How to turn on a computer using the router's WEB-interface ###
You can turn on a computer on the local network from the <a href='http://my.router/Advanced_WOL_Content.asp'>WEB-interface</a> - just press **Wake up** opposite to the necessary device from the list or by entering its MAC-address in the appropriate field.

### How to turn on a computer on the local network using the script ###
Add the following cron task (<a href='https://code.google.com/p/rt-n56u/wiki/CommonTips#Using_the_built-in_scheduler_(crond)'>read about cron daemon</a>):
```
00 06 * * * /usr/sbin/ether-wake -i br0 XX:XX:XX:XX:XX:XX
```
Where `00 06 * * *` - time in <a href='http://wiki.linuxquestions.org/wiki/Crontab#Event_lines'>crontab format</a>, а XX:XX:XX:XX:XX:XX - MAC-address of the computer that you want to wake up on a schedule.

---



## Capture images from WEB-camera connected to the router`s USB-port ##
1. Setting up <a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureEntware'>Entware</a>

2. Verify that WEB-camera is on <a href='http://www.ideasonboard.org/uvc/#devices'>the list of supported devices</a> (otherwise the camera may don`t work with your router).

3. Connect your camera to router.

4. Connect to the router through Telnet/SSH

5. Run in console:
```
# modprobe uvcvideo
```
Before you continue, make sure that there was a video device / dev/video0. To check, you can run:
```
# ls /dev/video*
```
If the result will be "No such file or directory", it means that the camera is not supported by the driver uvcvideo.

6. Install the package **motion**.
```
# opkg update
# opkg install motion
```

7. <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips#How_do_I_edit_the_scripts/configuration_files?'>Edit</a> the file /opt/etc/motion.conf. It contains a lot of parameters, the most important are:
```
stream_localhost (on/off) - must be set to *off* to be able to get access to the video stream from the local network
stream_port (integer) - port of stream, the default is 8081
output_pictures (on/off) - is need to save snapshots
target_dir (путь) - directory to store all snapshots; you must specify an existing folder on disk. For example, if you specify /media/AiDisk_a1, files will be stored in the root of the first drive connected to the USB.
```

8. <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips#How_do_I_edit_the_scripts/configuration_files?'>Edit</a> the file /etc/storage/started\_script.sh, append the following line
```
modprobe uvcvideo
```
Run in console:
```
# mtd_storage.sh save
```
Now the camera will be initialized when you start / restart the router

9. Reboot the router or run in console:
```
# /opt/etc/init.d/S99motion start
```

10. Go to <a href='http://my.router:8081'>camera`s page</a>

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **WARNING! When you change the settings in the file /opt/etc/motion.conf you must restart the service of camera`s stream management (or restart the router) to apply the new values:
```
# /opt/etc/init.d/S99motion restart
```**

---



## Access to a scanner/MFP connected to the router`s USB-port ##
To configure the scanner use <a href='http://code.google.com/p/rt-n56u/wiki/HowToInstallSane'>this algorithm</a>

---



## Connecting MFP Samsung (for example, SCX-3400W) to the router via Wi Fi ##
To set-up your Samsung printer’s wireless settings with your computer follow the guide below:

1. First make sure the USB cable is connected to your computer and the printer

2. Then turn on your computer, printer and  <a href='http://192.168.1.1/Advanced_Wireless2g_Content.asp'>Wi Fi radio module on the router</a>

3. Then install the your printer’s driver (use the CD that came with your printer)

4. Then during installation you will be ask how do you want your printer connected choose "Wireless network setup with a USB cable" in "Connect Printer" and click Next.

5. Then when your computer sees your wireless connection connect to it then click next

6. If your printer supports Wi-Fi Direct, its corresponding screen will appear. Click Ok and Next.

7. When the wireless network set up is completed, disconnect the USB cable between the computer and machine. Click Next.

8. Click Next when the Printers Found window

9. Select the components to be installed. Click Next.


You should then be able to connect when with the printer when it is done.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **Note.** You might need to set the region "USA" in the properties of router`s Wi Fi point.

---



## Access to the printer HP Laser Jet connected to USB-port ##
The printers series HP LaserJet 1xxx/2xxx immediately after power on don't have the firmware. When the operating system detects a printer, it should "download" the necessary firmware to it and then work with it as with the simple printer. The same functions must execute our router.

If you want to use the printers series HP LaserJet 1xxx/2xxx connected to router's USB-port from your PC, you can use this algorithm based on connection the HP LaserJet 1022 (similarly for other models).

1. Setting up <a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureEntware'>Entware</a>

2. Connect to the router through Telnet/SSH

3. Create folder /opt/share/firmware. To do this, run in console:
```
# mkdir /opt/share/firmware
```

4. Copy the firmware for your printer into the directory /opt/share/firmware (you can dowload it <a href='http://files.rt-n56u.googlecode.com/git/hplj/'>here</a>. For the HP LaserJet 1022 you need the file <a href='http://files.rt-n56u.googlecode.com/git/hplj/sihp1022.dl'>sihp1022.dl</a>

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **WARNING!** Here and further instead of sihp1022.dl you must specify the correct name of the firmware file for your printer!!!

```
# wget http://files.rt-n56u.googlecode.com/git/hplj/sihp1022.dl -P /opt/share/firmware
```

5. <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips?wl=en#How_do_I_edit_the_scripts/configuration_files?'>Edit</a> the file /opt/bin/on\_hotplug\_printer.sh by changing the string
```
lpfw="/opt/share/firmware/sihp1020.dl"
```
to
```
lpfw="/opt/share/firmware/sihp1022.dl"
```

6. set the option "Enable TCP/IP RAW port?" to "Yes" in <a href='http://my.router/Advanced_Printer_others.asp'>WEB-interface</a>:

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/printer-058-en.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/printer-058-en.png)


7. Connect the printer to the router through the USB-cable and turn on it. Each time you turn on the printer it will boot firmware, which can be seen as the additional printer initialization.

8. Set up a connection to a network printer for TCP/IP port 9100 on your computer (you can use <a href='http://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/print_add_tcpip_port.mspx?mfr=true'>this instruction</a> or  <a href='http://technet.microsoft.com/en-us/library/cc728320(v=ws.10).aspx'>this</a>)

---



## Checking ink level of your printer attached to router's to USB-port ##
If you want to check the ink level of printer attached to your router , you can use the utility _ink_ from Entware. For install the _ink_ utility you can this algorithm:

1. Setting up <a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureEntware'>Entware</a>

2. Run in console:
```
# opkg update
# opkg install ink
# opkg install libinklevel
```

3. For check the ink level of your printer run in console:
```
# ink -p usb
```

---



## Use several/other DDNS-servers ##
If you want using several DDNS-servers or the desired DDNS-server don`t present in the list of supported servers, you can add support for its by using this algorithm.

1. Disable DDNS-client in <a href='http://my.router/Advanced_ASUSDDNS_Content.asp'>WEB-interface</a>

2. Create directory /opt/etc/ddns:
```
# mkdir /opt/etc/ddns
```

3. In directory /opt/etc/init.d create script S02ddns with this content (you can use <a href='http://dl.dropboxusercontent.com/u/44733876/googlecode/share/S02ddns'>this script</a>):
```
#!/bin/sh
 
func_start()
{
        echo "Start DDNS services"
        # insert your custom code below
        inadyn --input_file /opt/etc/ddns/inadyn.conf  # start DDNS-service for server DDNS 1
        inadyn --input_file /opt/etc/ddns/inadyn2.conf  # start DDNS-service for server DDNS 2
}
 
func_stop()
{
        echo "Stop DDNS services"
        # insert your custom code below
        killall -q inadyn
}
 
case "$1" in
start)
        func_start
        ;;
stop)
        func_stop
        ;;
restart)
        func_stop
        func_start
        ;;
*)
        echo "Usage: $0 {start|stop|restart}"
        exit 1
        ;;
esac
```

4. In directory /opt/etc/ddns create configuration file(s) inadyn.conf (inadyn2.conf and so on, respectively the number of required records for DDNS-Server).
For example, inadyn.conf for service dyndns.com:
```
dyndns_system dyndns@dyndns.org
update_period_sec 1800 # check for a new IP every 30 minutes
username ****    # login for server dyndns.com
password ****    # password for server dyndns.com
alias ****.dyndns.org    # alias (host name) for server dyndns.com
background
ip_server_name checkip.ns.zerigo.com /
cache_file /opt/etc/ddns/ddns.cache
# log_file /opt/etc/ddns/inadyn.log   # if you want to inadyn recorded their results in own log, uncomment this line, the default will record in the system log
```
For example, inadyn.conf for service no-ip.com:
```
dyndns_system default@no-ip.com
update_period_sec 1800 # check for a new IP every 30
username ****    # login for server no-ip.com
password ****    # password for server no-ip.com
alias ****.sytes.net    # alias (host name) for server no-ip.com
background
cache_file /opt/etc/ddns/ddns2.cache
# log_file /opt/home/admin/inadyn.log
```
You should replace the asterisks on your accounts data

---



## Custom MAC address filtering ##
Assume, your child spends too much time in the internet. And you'd like to limit access time by schedule.

All easily configured through <a href='http://my.router/Advanced_MACFilter_Content.asp'>WEB-interface</a>:

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/macfilter-040-en.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/macfilter-040-en.png)


![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  **Note.** Time can not be set with the transition through the midnight. If you want to specify a range 22:30-07:00, split it into two rules:
  1. 22:30-23:59
  1. 00:00-07:00



Keep in mind that nowadays children are very smart. If your "genius" changes mac address on his machine, the rule is not be applied to his machine any more. So you should properly configure your dhcp server.

---



## Using a script to filter traffic using MAC addresses of devices ##
1. <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips#How_do_I_edit_the_scripts/configuration_files?'>Edit</a> the file /etc/storage/post\_iptables\_script.sh  and add to it lines in the following format:
```
iptables -I FORWARD -m mac --mac-source 11:22:33:44:55:66 -j DROP
```
where 11:22:33:44:55:66 - MAC-address of the device for which you want to block traffic.
**FORWARD** is used if you want to filter transit (passing through a router) traffic.

If you want to block access to the router, use the directive **INPUT**:
```
iptables -I INPUT -m mac --mac-source 11:22:33:44:55:66 -j DROP
```

Save file.

2. Run in console
```
# mtd_storage.sh save
```

---



## Restricting access to undesirable content using Yandex.DNS ##
Many users want to protect themselves or their children from adult sites. The algorithms of family search from Yandex are able to identify erotica and porn. When a user opens a porn site on your computer or network with <a href='http://dns.yandex.ru/'>Yandex.DNS</a> in the "Family" mode, he only see the parking page.

All easily configured through <a href='http://my.router/Advanced_DHCP_Content.asp'>WEB-interface</a>:

1. Select in the left pane <a href='http://my.router/Advanced_DHCP_Content.asp'>Advanced Settings -> LAN -> DHCP Server</a> <br>
2. Select "Custom Configuration File "dnsmasq.conf"". <br>
3. In the opened window to the end of the script append the text: <br>
<pre><code>### Yandex.DNS for kids Smartphone <br>
dhcp-host=AA:BB:CC:DD:EE:FF,set:kids <br>
# for host №2:<br>
# dhcp-host=A2:B2:C2:D2:E2:F2,set:kids <br>
dhcp-option=tag:kids,option:dns-server,77.88.8.7,77.88.8.3 <br>
</code></pre>
where AA:BB:CC:DD:EE:FF - MAC-address of the device for which you want to enable protection from "adult" material <br>
4. Click <b>Apply</b>. <br>

<b>Note.</b> You can select "Safe" mode by specifying the servers 77.88.8.88 and 77.88.8.2. For further details about modes, visit the website  <a href='http://dns.yandex.ru/'>Yandex.DNS</a>
<hr />


<h2>Using a second router to increase the coverage area of ​​Wi Fi</h2>
Device #1 connected to the Internet. Standard mode "Router". For example, LAN subnet 192.168.1.0 and address of Device #1 is 192.168.1.1.<br>
<br>
Device #2 - remote. Switch to AP-mode in <a href='http://my.router/Advanced_OperationMode_Content.asp'>WEB-interface</a>. It is better to assign a fixed address, such as 192.168.1.2 and this address add to the exception list on DHCP on Device #1 or distribute addresses from 192.168.1.3.<br>
<br>
<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png' />  <b>IMPORTANT!!! All routers are configured for this scheme must have different names!!! The "Device Name" can be changed in</b><a href='http://my.router/Advanced_AiDisk_others.asp'><b>WEB-interface</b></a>

<h3>Example of WDS</h3>

On Device #1 point is configured in <a href='http://my.router/Advanced_WMode2g_Content.asp'><b>Bridge</b> tab</a> (<a href='http://my.router/Advanced_WMode_Content.asp'><b>or for 5GHz</b></a>) as "AP & WDS". Channel is fixed.<br>
<br>
On Device #2 point is configured as "WDS only", scan the air, add BSSID of Device #1 to list. If you plan that customers will use this same point in the Device # 2, then configure it as an "AP & WDS". Then point will connect to Device #1 WDS as a client and at the same time be able to work as a point.<br>
<br>
<h3>Example of AP-Client</h3>

On Device #1 point is configured in <a href='http://my.router/Advanced_WMode2g_Content.asp'><b>Bridge</b> tab</a> (<a href='http://my.router/Advanced_WMode_Content.asp'><b>or for 5GHz</b></a>) as "AP". Channel is fixed.<br>
<br>
On Device #2 point is configured as "AP-Client Only", scan the air, add BSSID of Device #1 to list. If you plan that customers will use this same point in the Device # 2, then configure it as an "AP & AP-Client". Then point will connect to Device #1 WDS as a client and at the same time be able to work as a point.<br>
<hr />


<h2>How to configure xUPnPd mediaserver</h2>
Modern TVs have built-in network interfaces support DLNA, in other words, can play media (images, video, music) that are transmitted over the network.<br>
<br>
To watch IPTV on your TV you should configure on your router DLNA-server <a href='http://xupnpd.org/t/'>xUPnPd</a>.<br>
<br>
<h3>How to configure built-in xUPnPd mediaserver</h3>
If you install to your router <a href='http://code.google.com/p/rt-n56u/downloads/list'>the firmware from the repository</a>, it already contains the integrated mediaserver xUPnPd. <br>
In this case, the server xUPnPd is configured through <a href='http://my.router/Advanced_IPTV_Content.asp'>WEB-interface</a>:<br>
<br>
<ol><li>At first, select in the left pane <a href='http://my.router/Advanced_IPTV_Content.asp'>Advanced Settings -> LAN -> IPTV</a> <br>
</li><li>Specify the port for DLNA-broadcast content (eXtensible UPnP agent (xupnpd), Web port). <br>
</li><li>Click <b>Apply</b>. <br>
</li><li>Perform the necessary xUPnPd mediaserver settings (including adding playlists), using a link <b>Web status</b>. <br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/xupnpd-040-en.png' /></li></ol>


<h3>How to configure xUPnPd mediaserver from Entware</h3>
With <a href='http://code.google.com/p/rt-n56u/wiki/HowToMakeFirmware'>do the build firmware yourself</a>, can be a situation that you have disabled xUPnPd when building for other services because of lack of space in the flash.<br>
In this situation, you may install xUPnPd mediaserver from Entware.<br>
<br>
To do this, execute in a terminal:<br>
<pre><code># opkg update<br>
# opkg install xupnpd<br>
</code></pre>

Start xUpnpd:<br>
<pre><code># /opt/etc/init.d/S94xupnpd start <br>
</code></pre>
After installation the xUpnpd you may need to <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips#How_do_I_edit_the_scripts/configuration_files?'>edit its configuration files</a>, are located in folder  /opt/share/xupnpd (All settings can be done through <a href='http://my.router:4044'>WEB-interface</a>).<br>
<hr />


<h2>How to configure miniDLNA mediaserver</h2>
ReadyMedia (formerly <a href='http://sourceforge.net/projects/minidlna/'>MiniDLNA</a> - is a server software with the aim of being fully compliant with <a href='http://en.wikipedia.org/wiki/Universal_Plug_and_Play#UPnP_AV_standards'>UPnP/DLNA</a> clients. It is developed by a NETGEAR employee for the ReadyNAS product line.<br>
It is not in any way endorsed by the Digital Living Network Alliance®.<br>
<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png' />  When using a mediaserver UPnP/DLNA is recommended to have SWAP-partition, because in the process of creating the database of media content is consumed a large amount of RAM.<br>
<br>
If you install to your router <a href='http://code.google.com/p/rt-n56u/downloads/list'>the firmware from the repository</a>, You should note that the mediaserver miniDLNA is integrated into the firmware RT-N56U_x.x.x.x-xxx<i><b>dlna</b>.zip (for RT-N65U router is the version RT-N65U_x.x.x.x-xxx</i><b>full</b>.zip). <br>
The mediaserver miniDLNA is configured through <a href='http://my.router/Advanced_AiDisk_others.asp'>WEB-interface</a>:<br>
<br>
<ol><li>Connect the USB-drive with media content <br>
</li><li>Select <a href='http://my.router/Advanced_AiDisk_others.asp'>Advanced Settings -> USB Application -> Common setting</a> <br>
</li><li>Switch on UPnP/DLNA Media Server <br>
</li><li>Specify the media sources (you can select its from the drop-down list) <br> <br> <img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png' />  If you are using a shared folder for audio, video and images, you need to specify only the path to this folder and leave the other fields blank. <br>
</li><li>Click <b>Apply</b>. <br> <br> <img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/dlna-en.png' /> <br>
</li><li>The statistics of MiniDLNA media server can be obtained by using the link <b><i>Web status</i></b>. <br></li></ol>

If the path to the content are correct, all new files will be updated automatically, regardless of the "Rebuild Database Content on Start".<br>
<br>
"<b>Rebuild Database Content on Start</b>" has meaning only in these situations:<br>
<ul><li>When you turn on the MiniDLNA manually<br>
</li><li>When you connect the drive when the MiniDLNA is enabled<br>
</li><li>When running the router with the MiniDLNA is enabled</li></ul>

MiniDLNA starts to re-scan the database if the database on the drive is corrupted or missing (or "Rebuild Database Content on Start" is set to "Force rebuild  database").<br>
<br>
<i><b>Note.</b>  Sometimes, after changing the version of miniDLNA, the structure of its database is changed and mediaserver stops working. In this case, you must manually delete the database in the directory <code>/media/Main/.dms</code> (where <code>Main</code> - the volume label of the partition with media content). In this directory miniDLNA media server also places its log.</i>
<hr />


<h2>How to configure Transmission</h2>
<a href='http://www.transmissionbt.com/'>Transmission</a> is free <a href='http://www.bittorrent.org/'>BitTorrent</a>-client which features a simple interface.<br>
<a href='http://www.transmissionbt.com/'>Transmission</a> allows users to download files from the Internet and upload their own files or torrents.<br>
<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png' />  You can install Transmission to your router Asus RT-N56U/RT-N65U, but you must remember that the CPU in a subject is not adapted for these tasks and at the same time it will be loaded at 100%. It is also strongly recommended for downloads "native" file system - EXT2/EXT3/EXT4 (EXT4 is preferred). To prepare the USB-drive, you can use <a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureEntware#Using_the_Router_to_Format_the_Disk_Drive'>this manual</a> (it should be noted that, most likely, you do not need the SWAP-partition)).<br>
<br>
<h3>How to configure built-in Transmission</h3>
If you install to your router <a href='http://code.google.com/p/rt-n56u/downloads/list'>the firmware from the repository</a>, it already contains the integrated BitTorrent-client Transmission. <br>
In this case, the Transmission is configured through <a href='http://my.router/Advanced_AiDisk_others.asp'>WEB-interface</a>:<br>
<br>
<ol><li>Connect the USB-drive and, if necessary, <a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureEntware#Using_the_Router_to_Format_the_Disk_Drive'>format it to EXT4 file system</a>. <br>
</li></ol><blockquote>2. Create folder <b>transmission</b> at the root of created partition: <br>
<blockquote>2.1. Select <a href='http://my.router/Advanced_AiDisk_ftp.asp'>Advanced Settings -> USB Application -> FTP Share</a>. <br>
2.2. Create folder <b>transmission</b> at the root of the desired partition <br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/web-add-folder-en.png' />  <br>
</blockquote>3. Select <a href='http://my.router/Advanced_AiDisk_others.asp'>Advanced Settings -> USB Application -> Common setting</a> <br>
4. Switch on Transmission. <br>
5. Specify the port to connect the peers (in this case the specified port will be automatically open). <br>
6. Specify the RPC port for management (on the given port will be available WEB-based management of the Transmission from the LAN). <br>
7. Click <b>Apply</b>. <br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/transmission-064-en.png' /> <br>
8. Perform the necessary Transmission's settings using a link <b>Web control</b>. <br></blockquote>


<h3>How to configure Transmission from Entware</h3>
With <a href='http://code.google.com/p/rt-n56u/wiki/HowToMakeFirmware'>do the build firmware yourself</a>, can be a situation that you have disabled the Transmission when building for other services because of lack of space in the flash.<br>
In this situation, you may install the Transmission from Entware.<br>
<br>
To do this, execute in a terminal:<br>
<pre><code># opkg update<br>
# opkg install transmission<br>
</code></pre>

<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png' />  To configure Transmission is most convenient to use the <a href='http://code.google.com/p/transmisson-remote-gui/'><b>Transmission Remote GUI</b></a>
<hr />


<h2>Connect to router`s WEB-interface using SSH-tunnel</h2>
If you should have access to the router`s WEB-interface from the Internet, then surely you can open the port for the Web Access from WAN.<br>
<br>
However, in this situation your password will be sent as plain text that is not safe.<br>
<br>
There is a secure solution for this problem.<br>
<br>
1. Configure <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips#Installation_and_Usage_the_Terminal_Application'>terminal access</a>

2. Allow access to SSH from WAN. In <a href='http://my.router/Advanced_BasicFirewall_Content.asp'>WEB-interface</a> switch on "Access SSH server from WAN?" and specify "SSH Server Port from WAN":<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/webssh-042-en.png' />

3. If you are using PUTTY, on the tab Connection -> SSH -> Tunnels select "Local", in the field "Source port" insert the value "8888" in the field "Destination" write "192.168.1.1:80". Then press the <b>Add</b>:<br>
<blockquote><img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/putty_web.png' /></blockquote>

4. Establish SSH-session using port from the p.2.<br>
<br>
5. To access the WEB-interface in browser specify the address <a href='http://localhost:8888'>http://localhost:8888</a>
<hr />


<h2>Connect from the Internet to the LAN located behind the router, using the integrated VPN-Server</h2>
If you should have access to the local network from the Internet, you can <a href='http://code.google.com/p/rt-n56u/wiki/BuiltInVpnServer'>configure the VPN-server included in the firmware</a>.<br>
<hr />


<h2>FTP port forwarding to a dedicated FTP server in the LAN subnet</h2>
If you should have access to FTP-server located in the local network from the Internet, you can do it in Web-Interface at page <a href='http://my.router/Advanced_VirtualServer_Content.asp'>Advanced Settings -> WAN -> Port Forwarding</a>:<br>
<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/Advanced-VirtualServer-Content-en.png' />
<blockquote><img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png' />  <i>You should specify the "Local Port" only if it is different from the value specified in the "Port Range".</i></blockquote>


If this FTP-server is running on a port other than 21, you must add this port in <b>FTP ALG</b> at page <a href='http://my.router/Advanced_Netfilter_Content.asp'>Advanced Settings -> WAN -> Netfilter</a>:<br>
<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/Advanced-Netfilter-Content-en.png' />
<hr />


<h2>How to configure FTP-server to access the USB-connected storage devices over WAN</h2>
If you need to access a USB-drives connected to the router from local network (or from Internet), you can use the FTP-server integrated into the router`s firmware. You can use this algorithm.<br>
<br>
1. At first, select in the left pane <a href='http://my.router/Advanced_AiDisk_others.asp'>Advanced Settings -> USB Application -> Common setting</a>

<ol><li>1. Switch on "Enable FTP Server?"</li></ol>

<ol><li>2. Select "Share Access Mode:" - "Access with account" (<i>Use anonymous access to Internet-access is not recommended!</i>)</li></ol>

<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/ftp1-061-en.png' />

2. Select <a href='http://my.router/Advanced_AiDisk_ftp.asp'>Advanced Settings -> USB Application -> FTP Share</a>

<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/ftp2-061-en.png' />

<blockquote>2.1. Adding users</blockquote>

<blockquote><img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/web-add-user-en.png' /></blockquote>

<blockquote>2.2. Create the directories (if needed)</blockquote>

<blockquote><img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/web-add-folder-en.png' /></blockquote>

<blockquote>2.3. On the left side, select the user and specify the access to the necessary resources for him (on the right).</blockquote>

3. Select <a href='http://my.router/Advanced_BasicFirewall_Content.asp'>Advanced Settings -> Firewall -> General</a>

<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/ftp3-061-en.png' />

<blockquote>3.1. Switch on "Access FTP Server from WAN?"</blockquote>

<blockquote>3.2. Specify "FTP Server Port from WAN:" (default 21)</blockquote>

4. To access from the LAN enter in the browser (or FTP-client) <a href='ftp://my.router'>ftp://my.router</a> or <a href='ftp://user:password@my.router'>ftp://user:password@my.router</a> (where <i>user</i> and <i>password</i> are specified in Section 2.1). For access from the Internet instead of the my.router write your external IP-address or FQDN-hostname.<br>
<hr />


<h2>How to configure Samba-server to access the USB-connected storage devices over LAN</h2>
<a href='http://www.samba.org/'>Samba</a> is Free Software licensed under the GNU General Public License, the Samba project is a member of the Software Freedom Conservancy.<br>
Since 1992, Samba has provided secure, stable and fast file and print services for all clients using the SMB/CIFS protocol, such as all versions of DOS and Windows, OS/2, Linux and many others.<br>
<br>
<h3>How to configure Samba-server by using the WEB-interface</h3>
If you need to access a USB-drives connected to the router from network devices (such as computers running Windows), you must configure the Samba-server integrated into the router`s firmware.<br>
<br>
1. At first, select in the left pane <a href='http://my.router/Advanced_AiDisk_others.asp'>Advanced Settings -> USB Application -> Common setting</a>

2. Switch on "Enable SMB Server?"<br>
<br>
3. If necessary, change the name of the Work Group<br>
<br>
4. Select "Share Access Mode:" - anonymous access (without account) or access with account<br>
<br>
5. If the router should provide the function of displaying the list of computers and shared resources on a network, then activate the item "Enable local Master Browser?"<br>
<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/samba1-047-en.png' />


If in step 4 has been selected access by using an account, then:<br>
<br>
6. Select <a href='http://my.router/Advanced_AiDisk_samba.asp'>Advanced Settings -> USB Application -> Network Neighborhood Share</a>

7. Add accounts and distribute the necessary permissions to directories (on the screenshot is not active, because anonymous access is selected)<br>
<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/samba2-047-en.png' />


<h3>Advanced configure for Samba-server</h3>
If you need to make advanced settings for Samba-server, which are not represented in the Web-interface (for example, change the root of shared resources), it is necessary to make additional manipulation:<br>
<br>
1. <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips?wl=en#How_to_configure_Samba-server_by_using_the_WEB-interface'>Configure Samba-server</a>

2. Select <a href='http://my.router/Advanced_AiDisk_others.asp'>Advanced Settings -> USB Application -> Common setting</a> and switch off "Enable SMB Server?"<br>
<br>
3. Run terminal. Copy files from /etc/samba to /opt/etc/samba<br>
<br>
4. In directory /opt/etc/init.d create script S08samba with this content (you can use <a href='http://dl.dropboxusercontent.com/u/44733876/googlecode/share/S08samba'>this script</a>):<br>
<pre><code>#!/bin/sh<br>
 <br>
prgmname1="/sbin/nmbd"<br>
prgmname2="/sbin/smbd"<br>
 <br>
# configfile=/full_path/configfile<br>
configfile="/opt/etc/samba/smb.conf"<br>
 <br>
PATH=/opt/sbin:/opt/bin:/opt/usr/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin <br>
 <br>
#location of pid-file<br>
nmbdpid="/var/run/nmbd.pid"<br>
smbdpid="/var/run/smbd.pid"<br>
 <br>
start() {<br>
        # Code here to start the program<br>
        mkdir -p /etc/samba<br>
        cp /opt/etc/samba/secrets.tdb /etc/samba/<br>
        cp /opt/etc/samba/smbpasswd /etc/samba/<br>
        ${prgmname1} -D -s ${configfile}<br>
        logger -t nmbd "started $prgmname1, conf: $configfile"<br>
        ${prgmname2} -D -s ${configfile}<br>
        logger -t smbd "started $prgmname2, conf: $configfile"<br>
        return 0<br>
}<br>
 <br>
stop() {<br>
        # Code here to stop the program and check it's dead<br>
        [ -f $nmbdpid ] &amp;&amp; kill `cat $nmbdpid` &amp;&amp; rm -f $nmbdpid<br>
        logger -t nmbd "service stopped"<br>
        sleep 1<br>
        [ -f $smbdpid ] &amp;&amp; kill `cat $smbdpid` &amp;&amp; rm -f $smbdpid<br>
        logger -t smbd "service stopped"<br>
        return 0<br>
}<br>
##########################start here##########################<br>
case "$1" in<br>
  start)<br>
        start<br>
        ;;<br>
  stop)<br>
        stop<br>
        ;;<br>
  restart)<br>
        logger -t Samba "nmbd &amp; smbd restart"<br>
        stop<br>
        sleep 2<br>
        start<br>
        ;;<br>
  *)<br>
        echo $"Usage: $0 {start|stop|restart}"<br>
        exit 1<br>
esac<br>
exit <br>
</code></pre>

5. <a href='http://code.google.com/p/rt-n56u/wiki/CommonTips#How_do_I_edit_the_scripts/configuration_files?'>Edit</a> the file /opt/etc/samba/smb.conf (examples can be found on <a href='http://www.samba.org/'>The Samba project website</a>)<br>
<br>
6. Start Samba-server (on start/reboot router the Samba-server will start automatically):<br>
<pre><code># /opt/etc/init.d/S08samba start <br>
</code></pre>
<hr />


<h2>How To mount SMB-resources from LAN?</h2>
Sometimes you need to access from the router to SMB-LAN resources (such as shared folders on Windows-based machine). This is possible, but you should know a few things.<br>
<br>
1. The firmware should include the CIFS-client. All firmwares with the prefix <code>nano</code> as well as all the standard firmwares for the router N56U not contain this functionality. You must select the correct version of firmware (with prefixes <code>base</code> or <code>full</code>) or <a href='https://code.google.com/p/rt-n56u/wiki/HowToMakeFirmware?wl=ru'>build firmware yourself</a> to include a necessary component (ie, in the file /opt/rt-n56u/trunk/.config uncomment <code>#CONFIG_FIRMWARE_INCLUDE_CIFS=y</code>)<br>
<br>
2. You must also run the modules needed to prepare and mount point. This can be done by executing the following commands in the console:<br>
<pre><code>modprobe des_generic<br>
modprobe cifs CIFSMaxBufSize=64512<br>
mkdir -p /media/cifs<br>
mount -t cifs \\\\{host}\\{share} /media/cifs -o username={user},password={pass}<br>
</code></pre>

You can enter this into <a href='http://my.router/Advanced_Tweaks_Content.asp'>the script "Run after Router started"</a> to perform these operations, whenever you turn on / restart the router.<br>
<br>
<ul><li>The <code>des_generic</code> module is needed to support Windows 7/8, otherwise you mount their shared resources in the log will be an error.<br>
</li><li>Backslash is a reserved character, so for entering UNC path like \\server\share, is needed shielding backslash. This is all according to the rules of the Unix-shell.<br>
<hr /></li></ul>


<h2>When you use the ping command in the console is lost access to WEB-interface</h2>
To run commands in addition to the terminal you can also use <a href='http://my.router/Main_AdmStatus_Content.asp'>the console</a>. However, it must be remembered that the interface waits when the command is finished.<br>
For example, in Linux, unlike Windows, the command <code>ping</code> running "endlessly" without returning the final result.<br>
Therefore, if you want to ping a host from <a href='http://my.router/Main_AdmStatus_Content.asp'>the console</a>, you must use the additional keys, ie, in the command line you need to write a command like:<br>
<pre><code>ping -c 3 host<br>
</code></pre>
<hr />


<h2>Using Authorized Keys</h2>
It is possible to sign into your router terminal without password and staying secure at the same time using SSH protocol.<br>
<br>
It is very simple for <b><i>Linux or MacOS users</i></b>.<br>
<br>
First, follow <a href='http://my.router/Advanced_System_Content.asp'><b>this link</b></a> and enable <b>SSH Server</b>.<br>
<br>
<i><b>For Linux or Mac OS users.</b></i> Open the terminal and generate new public and private key pair  (on your PC).<br>
<pre><code># cd ~/.ssh<br>
# ssh-keygen -t rsa<br>
<br>
Generating public/private rsa key pair.<br>
Enter file in which to save the key (/home/username/.ssh/id_rsa): n56u<br>
Enter passphrase (empty for no passphrase): <br>
Enter same passphrase again: <br>
Your identification has been saved in n56u.<br>
Your public key has been saved in n56u.pub.<br>
The key fingerprint is:<br>
83:f1:2a:b1:e4:51:0b:58:70:a3:06:3a:6a:f8:bf:d0 username@host<br>
The key's randomart image is:<br>
+--[ RSA 2048]----+<br>
|. ..+            |<br>
|.. = .           |<br>
|o + . o          |<br>
|oo   o =         |<br>
|o.  + o S        |<br>
|.. + + . .       |<br>
|  o E .          |<br>
|   o .           |<br>
|    o.           |<br>
+-----------------+<br>
</code></pre>

And copy them to router:<br>
<b>Make sure you are copying publuc key (filename.pub)</b>
<pre><code># ssh-copy-id -i ./n56u.pub admin@my.router<br>
</code></pre>
You'll be asked for password this time. If you try to sign into router after this operation, you would be passed by using your public and private keys.<br>
<br>
<b><i>If you use Windows OS</i></b>, you need to download the last version of <a href='http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html'><b>PuTTY</b></a>.<br>
Generate new keys, using <b>puttygen.exe</b> tool (you need to move your mouse <br>when pressed 'Generate').<br>
Save two generated files to disk. Copy public one to clipboard. Sing in to your router using Putty. (this time it will ask for password).<br>
<br>
make sure that directory <b>'/home/root/.ssh'</b> exists:<br>
<pre><code># ls -la /home/admin/.ssh<br>
</code></pre>
If there is an error, create this directory:<br>
<pre><code># mkdir -p /home/admin/.ssh<br>
</code></pre>

Then type:<br>
<pre><code># cat - &gt;&gt; /home/admin/.ssh/authorized_keys<br>
</code></pre>
Paste your public key to the terminal, then press 'Enter' and then press CTRL+D.<br>

Change directory rights:<br>
<pre><code># chmod -R 700 /home/admin/.ssh<br>
</code></pre>

That's it! Next time you wouldn't be asked for password.<br>
<br>
If you'd like to save your Authorized Keys to router flash (keys would be available when disk is not mounted), then you should do:<br>
<pre><code># cp /home/admin/.ssh/authorized_keys /etc/storage<br>
# mtd_storage.sh save<br>
</code></pre>
<hr />


<h2>Let your FTP server be secure</h2>
The SSH File Transfer Protocol (also Secret File Transfer Protocol, Secure FTP, or SFTP) is a network protocol that provides file access, file transfer, and file management functionality over any reliable data stream. It was designed by the Internet Engineering Task Force (IETF) as an extension of the Secure Shell protocol (SSH) version 2.0 to provide secure file transfer capability, but is also intended to be usable with other protocols.<br>
<br>
SFTP-server is built to firmware and all you need to do is to enable <a href='http://my.router/Advanced_System_Content.asp'><b>SSH server here</b></a>.<br>
<br>
If you'd like to use sFTP from the internet (outside your home network), enable 'Access SSH Server from WAN?' <a href='http://my.router/Advanced_BasicFirewall_Content.asp'><b>here</b></a>.<br>
<br>
Install any client, which provides sftp. For example, <a href='http://filezilla-project.org/'><b>Filezilla</b></a>.<br>
And connect to the router:<br>
<pre><code>host        your router local ip address<br>
username    admin<br>
password    YoUrSeCrEt<br>
port        22 (10022 from the internet)<br>
</code></pre>
<hr />


<h2>Create backup of directory /opt</h2>
First, stop all applications which started from /opt/etc/init.d. I think the easiest way to do it is to unmount disk in web GUI.<br>
So, go to <a href='http://my.router/'>http://my.router/</a>, click to the disk icon and press 'Remove'. Then login to the router using the terminal.<br>
<br>
<pre><code># mkdir /mnt/backup<br>
# mount -t ext3 /dev/sda1 /mnt/backup<br>
# cd /mnt/backup<br>
# tar -jcvf ./opt-backup.tar.bz2 ./opt<br>
# umount /mnt/backup<br>
</code></pre>

Then unplug the disk and plug-in again.<br>
<br>
If you'll need to restore data, then do almost the same:<br>
<pre><code># mkdir /mnt/backup<br>
# mount -t ext3 /dev/sda1 /mnt/backup<br>
# cd /mnt/backup<br>
# tar -jxvf ./opt-backup.tar.bz2<br>
# umount /mnt/backup<br>
</code></pre>
<hr />


<h2>What is the difference between routers Asus RT-N56U and RT-N65U?</h2>
Here is a summary table of differences:<br>
<br>
<br>
N56U:<br>
<ul><li>[+] 2 RGMII ports (max throughput 1.3Gbit/s on boths direction between WAN-LAN for IPoE and PPPoE).<br>
</li><li>[-] Unstable USB2 port (i think bug in PCB)<br>
</li><li>[-] Only 2T3R WiFi 5GHz<br>
</li><li>[-] 2T2R WiFi 2.4GHz control on main CPU (high CPU load on high speed transfers)<br>
</li><li>[-] 8MB Flash (is enough for router applications)</li></ul>


N65U:<br>
<ul><li>[+] 3T3R WiFi 5GHz<br>
</li><li>[+] 2T2R WiFi 2.4GHz on second CPU RT3352 (no main CPU load on high speed transfers)<br>
</li><li>[+] External USB3 chip (more stable, a bit more fast).<br>
</li><li>[+] 16MB Flash<br>
</li><li>[-] 1 RGMII port (max throughput 950Mbit/s on boths direction between WAN-LAN for IPoE and PPPoE).<br>
</li><li>[-] hardware issue with AP 2.4GHz on plug some USB HDD (RT3352 power issue on PCB)<br>
</li><li>[-] some noise from chokes on PCB<br>
<hr /></li></ul>


<h2>How to adjust the power of Wi Fi-signal?</h2>
The power of WiFi-signal regulated by the parameter  <a href='http://my.router/Advanced_Wireless2g_Content.asp'>TX Power Adjustment (%)</a> (<a href='http://my.router/Advanced_Wireless_Content.asp'>for 5GHz</a>.<br>
<br>
Available 6 steps to adjust TxPower (in fact weakening the power of the nominal value), which entered discretely from 0 to 100%:<br>
<ul><li>100-91: no weakening<br>
</li><li>90-61: weakening -1dB<br>
</li><li>60-31: weakening -3dB<br>
</li><li>30-16: weakening -6dB<br>
</li><li>15-10: weakening -9dB<br>
</li><li>9-0: weakening -12dB</li></ul>

The calibration levels for TxPower are registered in the EEPROM, on each copy they differ, are prescribed at the factory with the procedure ATE. Firmware does not affect the EEPROM.<br>
<br>
<br>
<br>
<br>

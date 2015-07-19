

### Preparation ###
First, make sure that network card of the machine you are going to wake supports Wake-On-Lan.
Second, configure the machine properly. Change its BIOS settings and make configuration in OS if needed.

Then, go to http://my.router/Advanced_Switch_Content.asp and set 'Green Ethernet?' to 'No'. (just disable 'Green Ethernet')

There are two ways to make wake-on-lan work via the internet.

### 1. Secure way ###
#### Using external applications ####
> Configure built-in Poptop server as <a href='http://code.google.com/p/rt-n56u/wiki/BuiltInVpnServer'><b>it is written here</b></a>.

> On client machine:
> Connect to the internet. Connect to your VPN server. Send the magic packet as you are in your home network.
> i.e.:
    * ip address - your lan broadcast address (192.168.1.255 by default)
    * port - 9
    * mac - the mac address of the machine you are going to wake

#### Using the command line ####
> Enable "Access SSH Server from WAN" on <a href='http://my.router/Advanced_BasicFirewall_Content.asp'><b>this page</b></a>.
> Connect to router from WAN using the terminal. Type:
```
 # ether-wake -b -i br0 aa:bb:cc:dd:ee:ff
```


### 2. Insecure way ###
If you don't want to use VPN server, you can install wol package. First, switch on Optware usage. (<a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureOptware'><b>learn here</b></a> how to configure Optware).

Then connect to the terminal and type:
```
# ipkg install http://rt-n56u.googlecode.com/files/wol-handler_0.4.1_noarch.ipk
```

Change listening port in settings if needed.
```
# nano /opt/etc/wol/settings.conf
```
It is set to 3636 by default.

Go to http://my.router/Advanced_VirtualServer_Content.asp. Enable 'Port forwarding'.
Add record like in the picture below.

![http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/wol.png](http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/wol.png)

Press 'Add', then press 'Apply'.

And start server in the terminal:
```
# /opt/etc/init.d/S20wol start
```

On client machine:
  * ip address - your external ip address or DDNS record name
  * port - 3636 (or another if you've changed it)
  * mac - the mac address of the machine you are going to wake

**Note: if you use the second way, it is a potential hole to hackers. Everyone can wake your machine if he knows your ip address and port (it is very easy to scan and get it)!**
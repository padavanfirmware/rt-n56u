

# Media Server in RT-N56U #
Most of you should know, that Minidlna is not included to "p" versions of firmware since v10.
It was done because it requires many libraries, which are too heavyweight to be included. The thing is that one can't use mediaserver, without a usb disk. That's why it was decided to remove it and put to the package to the external repository. It is quite easy to install it back to your system.

There are several stream servers avaliable in the Optware repository. But first, you should configure the environment of your router. Please, read <a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureOptware'><b>this wiki</b></a> to learn the process.

## uShare ##
**uShare** is a UPnP (TM) A/V & DLNA Media Server. It implements the server component that provides UPnP media devices with information on available multimedia files. uShare uses the built-in http server of libupnp to stream the files to clients.

### Installation details ###
  * Open the terminal, connect to your router via <a href='http://en.wikipedia.org/wiki/Telnet'>Telnet</a> (<a href='http://en.wikipedia.org/wiki/Secure_Shell'>SSH</a> maybe)
  * Type in the termanal:
```
# ipkg update
# ipkg install ushare
```
> > This will install the package.


> Then we need to edit configuration file.
```
# nano /opt/etc/ushare.conf
```
> And edit some variables:
```
...
USHARE_NAME=MyMediaServer
...
USHARE_PORT=49200
...
USHARE_DIR=/media/AiDisk_a1
...
ENABLE_WEB=yes
...
ENABLE_TELNET=no
...
ENABLE_DLNA=yes
...
```

> Then we need to change start-up script, because it doesn't stop properly.
> You can download <a href='http://rt-n56u.googlecode.com/svn/share/S99ushare'><b>working S99ushare</b></a> and edit source file yourself:
```
# nano /opt/etc/init.d/S99ushare
```

> Or you can use the following commands:
```
# cat /opt/etc/init.d/S99ushare > /opt/etc/init.d/K99ushare.bak
# wget -qc http://dl.dropboxusercontent.com/u/44733876/googlecode/share/S99ushare -O- | cat - > /opt/etc/init.d/S99ushare
```

> Start the server:
```
# /opt/etc/init.d/S99ushare start
```

> You can also perform remote control of uShare UPnP Media Server through its web interface. This let you define new content locations at runtime or update the currently shared one in case the filesystem has  changed. To disable this feature, change ENABLE\_WEB=no in /opt/etc/ushare.conf.
```
http://ip_address:port/web/ushare.html
```
> (ip\_address - is your router lan ip address, port - is USHARE\_PORT=49200)



## MiniDLNA ##
**MiniDLNA** (aka ReadyDLNA) is server software with the aim of being fully compliant with DLNA/UPnP-AV clients.

To install it simply use:
```
# ipkg install http://rt-n56u.googlecode.com/files/minidlna_1.0.23-2_mipsel.ipk
```

You can optionally change configureation file, but actually it is not required:
```
# nano /opt/etc/minidlna.conf
```

Start the server:
```
# /opt/etc/init.d/S98minidlna start
```



## xUPnPd ##
**xupnpd - eXtensible UPnP agent.** <br>
This program is a light DLNA Media Server which provides <code>ContentDirectory</code> service for sharing IPTV unicast streams over local area network (with udpxy for multicast to HTTP unicast conversion).<br>
The program shares UTF8-encoded M3U playlists with links over local area network as content of the directory.<br>
You can watch HDTV broadcasts (multicast or unicast) and listen Internet Radio in IP network without transcoding and PC.<br>
<br>
<h3>Multicast IPTV without transcoding (xupnpd+udpxy) was tested with</h3>
<ul><li>Ubuntu 10.04, Ubuntu 10.10, Ubuntu 11.04 as Media Server<br>
</li><li>D-Link DIR-320 (DD-WRT v24 preSP2 13064, mipsel), ASUS WL-500gP, <i><b>ASUS RT-N56U</b></i>, TP-LINK WR841ND as Media Server<br>
</li><li><code>Sony PlayStation3</code> as UPnP player<br>
</li><li><code>IconBit</code> HDS4L, WDTV Live as UPnP player<br>
</li><li>HTC Desire as UPnP player (Android 2.2 + UPnPlay + VPlayer)<br>
</li><li>Samsung UE46D6510, Samsung UE40D5000PW, Samsung LE40c550, LG PZ750 as player<br>
</li><li>Microsoft Windows Media Player 11 as UPnP player<br>
</li><li>Ubuntu 10.04 with VideoLAN as UPnP player</li></ul>

<h3>Requirements for ASUS RT-N56U</h3>
<ul><li>Firmware with optware support. You can find one in <a href='http://code.google.com/p/rt-n56u/downloads/list'><b>Downloads</b></a>. (Use stable version)<br>
</li><li>IPKG (Package Management System) should be configured on your USB device<br>
</li><li>Internet connection =)</li></ul>


<h3>Installation details</h3>
To install the package to your router follow these steps: <br>

<b>NOTE: As it was said before optware environment should be already installed and configured!</b>

<ul><li>Navigate your browser to <a href='http://my.router/Advanced_GWStaticRoute_Content.asp'>lan routes configure</a> and set <b>IPTV UDP Multicast to HTTP Proxy Port</b> to any value more than 1000 and less than 65000. For example 4022.</li></ul>

<ul><li>Open the terminal, connect to your router via <a href='http://en.wikipedia.org/wiki/Telnet'>Telnet</a> (<a href='http://en.wikipedia.org/wiki/Secure_Shell'>SSH</a> maybe)</li></ul>

<ul><li>Type in the termanal (see the last version of package in <a href='http://code.google.com/p/rt-n56u/downloads/list'><b>Downlods</b></a> section. Replace the link below with link to curren version):</li></ul>

<pre><code># ipkg install http://rt-n56u.googlecode.com/files/xupnpd_1-rc8_mipsel.ipk<br>
</code></pre>
<blockquote>The package will be installed and configured automatically. If you didn't change ip address of your router (192.168.1.1), you may skip next step.</blockquote>

<ul><li>Edit configuration file.</li></ul>

There are several ways to edit files in /opt directory.<br>
As for me, I prefer the next one.<br>
<br>
<pre><code># nano /opt/etc/xupnpd/xupnpd.lua<br>
</code></pre>

<b>configure the port of webserver:</b>

<pre><code>-- HTTP port for incoming connections<br>
cfg.http_port=4044<br>
</code></pre>

<b>change to true if you need this:</b>

<pre><code>-- XBox360 compatible mode <br>
cfg.xbox360=false<br>
</code></pre>

<b>change the device friendly name:</b>

<pre><code>-- Device name<br>
cfg.name='UPnP-IPTV'<br>
</code></pre>

<blockquote><i>You can also change other config values in this file if you like.</i></blockquote>

<ul><li>Start the daemon.</li></ul>

<pre><code># /opt/etc/init.d/S85xupnpd start<br>
</code></pre>

<ul><li>You can close terminal now, and go back to your browser.</li></ul>

<pre><code># http://my.router:4044<br>
</code></pre>

<hr />

<b>You'll see server configuration window.</b> <br> <br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/xupnpd1.png' />

<hr />

<b>Upload your playlist (m3u file).</b> <br><br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode-history/0cba18fc4559725ad3fbd14812807a79c8c194b4/pic/xupnpd2.png' />

Now switch on <code>PlayStation3</code>. You'll probably see 2 servers in XMB - RT-N56U and the new one - UPnP-IPTV. (maybe another name if you've changed it in xupnpd.lua). <br> <br> Choose this server, find your playlist, and have fun!! )<br>
<br>
<h3>Watch the video showing xupnpd in action</h3>
<a href='http://www.youtube.com/watch?feature=player_embedded&v=YomT03aNvro' target='_blank'><img src='http://img.youtube.com/vi/YomT03aNvro/0.jpg' width='425' height=344 /></a>
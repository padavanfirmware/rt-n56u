

**How To Install SANE _(Scanner Access Now Easy)_ On Routers RT-N56U/RT-N65U with**<a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureEntware'>ENTWARE</a>**---**


<a href='http://www.sane-project.org/'>SANE</a> stands for "Scanner Access Now Easy" and is an application programming interface (API) that provides standardized access to any raster image scanner hardware (flatbed scanner, hand-held scanner, video- and still-cameras, frame-grabbers, etc.).

---


1. At first, you must check that your scanner or MFP is supported in <a href='http://www.sane-project.org/sane-mfgs.html'>SANE</a>.

2. Install Sane-Backends:
```
# opkg update
# opkg install sane-backends
```

3. Install Sane-Frontends:
```
# opkg update
# opkg install sane-frontends
```

4. Power-On (reconnect) your scanner/MFP and checks that the router identified it. If all is well, we see this result (for example):
```
/opt/home/admin # scanimage -L
device `hpljm1005:libusb:001:002' is a Hewlett-Packard LaserJet M1005 multi-function peripheral
```

5. Sane works with server inetd or xinetd. In considered firmware integrated server inetd, so we will use it.
To automatically start the inetd on startup and reboot the router, add the following lines to the script /etc/storage/started\_script.sh:
```
############### inetd.conf file create ###################
# if app not exist
	if [ ! -f /usr/sbin/inetd ]; then
	    exit 0
	fi
	if [ -n "`pidof inetd`" ] ; then
		# stop daemon
	killall -q inetd
	fi
	Login=`nvram get http_username`
	touch /etc/inetd.conf
	echo "sane-port stream tcp nowait $Login /opt/sbin/saned saned" > /etc/inetd.conf
	/usr/sbin/inetd -R 30 -q 64 /etc/inetd.conf
 
##########################################################
```

When the router will be reboot, the file /etc/inetd.conf will be created with the parameters necessary to run SANE on startup inetd.

6. Edit file /opt/etc/sane.d/saned.conf.  <br>
6.1. Uncomment following line:<br>
<pre><code>data_portrange = 10000 - 10100<br>
</code></pre>
6.2. Edit the range of IP addresses on the local network which provides access to SANE. For example, in the section <i>Access list</i> add network:<br>
<pre><code>192.168.1.0/24<br>
</code></pre>

7. Install a graphical frontend for SANE at your computer. If your PC OS is Windows, it can be <a href='ftp://ftp2.sane-project.org/pub/sane/old-ftp.sane-project.org/xsane/'>xSane</a>, <a href='http://sanetwain.ozuzo.net/'>SaneTwain</a> or <a href='http://sourceforge.net/projects/sanewinds/'>SANEWinDS</a>, and if Linux - <a href='ftp://ftp2.sane-project.org/pub/sane/old-ftp.sane-project.org/xsane/'>xSane</a>. <br>
If you are using xSane as frontend, then do not forget to edit sane\etc\sane.d\net.conf (for Windows) or /etc/sane.d/net.conf (for Linux), adding a router:<br>
<pre><code># This is the net config file.  Each line names a host to attach to.<br>
# If you list "localhost" then your backends can be accessed either<br>
# directly or through the net backend.  Going through the net backend<br>
# may be necessary to access devices that need special privileges.<br>
# localhost<br>
192.168.1.1<br>
</code></pre>



<hr />
Main Author: <b>Volt1</b>
<hr />


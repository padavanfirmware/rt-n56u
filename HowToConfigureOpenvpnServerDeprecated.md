


---


## About OpenVPN ##
<a href='http://www.openvpn.net/'><b>OpenVPN</b></a> is a full-featured open source SSL VPN solution that accommodates a wide range of configurations, including remote access, site-to-site VPNs, Wi-Fi security, and enterprise-scale remote access solutions with load balancing, failover, and fine-grained access-controls. Starting with the fundamental premise that complexity is the enemy of security, OpenVPN offers a cost-effective, lightweight alternative to other VPN technologies that is well-targeted for the SME and enterprise markets.

This package version is preconfigured to be used on Asus RT-N56U with custom firmware by Padavan.
Client is required to provide account information (login and password).

### With OpenVPN, you can: ###
  * tunnel any IP subnetwork or virtual ethernet adapter over a single UDP or TCP port
  * configure a scalable, load-balanced VPN server farm using one or more machines which can handle thousands of dynamic connections from incoming VPN clients
  * use all of the encryption, authentication, and certification features of the OpenSSL library to protect your private network traffic as it transits the internet
  * use any cipher, key size, or HMAC digest (for datagram integrity checking) supported by the OpenSSL library
  * choose between static-key based conventional encryption or certificate-based public key encryption
  * use static, pre-shared keys or TLS-based dynamic key exchange
  * use real-time adaptive link compression and traffic-shaping to manage link bandwidth utilization
  * tunnel networks whose public endpoints are dynamic such as DHCP or dial-in clients
  * tunnel networks through connection-oriented stateful firewalls without having to use explicit firewall rules
  * tunnel networks over NAT
  * create secure ethernet bridges using virtual tap devices, and control OpenVPN using a GUI

## Requirements for ASUS RT-N56U ##
  * Firmware with optware support. You can find one in <a href='http://code.google.com/p/rt-n56u/downloads/list'><b>Downloads</b></a>
  * IPKG (Package Management System) should be configured on your USB device. You can <a href='http://code.google.com/p/rt-n56u/wiki/HowToConfigureOptware'><b>read this wiki</b></a> to learn how to install and use <a href='http://en.wikipedia.org/wiki/Optware'><b>Optware</b></a>.

OpenVPN runs on Linux, Windows 2000/XP/Vista/7 and higher, OpenBSD, FreeBSD, NetBSD, Mac OS X, and Solaris.


## Installation process ##
This package is already preconfigured and you need to do only few steps to use the server.
To install the package to your router follow these steps:
**NOTE: As it was said before optware environment should be already installed and configured!**

Open terminal, connect to your router via <a href='http://en.wikipedia.org/wiki/Telnet'><b>Telnet</b></a> (<a href='http://en.wikipedia.org/wiki/Secure_Shell'><b>SSH</b></a> maybe)

Type in terminal:

```
ipkg install http://rt-n56u.googlecode.com/files/openvpn_2.2.2-1_mipsel.ipk
```

The package will be installed and configuration process will be started.

You will be asked to enter some information. Don't be afraid, it is required by OpenSSL for <a href='http://en.wikipedia.org/wiki/Certificate_authority'><b>Certificate authority</b></a>. You can provide any information here, and actually you can leave most fields blank.
There is a default value in `[  ]`. If you'd like to set value by default, you should just press Enter. If you'd like to leave a field blank you need to type '.' (without quotes) and press Enter.

The form:
```
Enter country name ( 2 letter code ) [ US ] : US
Enter province ( some state/region ) [ ] : CA
Enter city [ ] : SanFrancisco
Enter organization [ router ] : Fort-Funston
Enter organization unit [ ] : 
Enter Common Name ( eg, YOUR name ) [ admin ] : Alex
Enter email [ admin@my.router ] : me@myhost.mydomain
```

<b>Note: 'Common Name' can't be blank!</b>

Then, you will be asked if information is correct. Type _**y**_ or _**yes**_ if it is, _**n**_ or _**no**_ if you need to correct anything.

The next documents will be created in **/opt/etc/openvpn/keys**:
```
Root CA certificate		ca.crt
Root CA key			ca.key
Server Certificate		server.crt
Server Key			server.key
Diffie Hellman parameters	dh1024.pem
Client Certificate		client.crt
Client Certificate		client.key
```

The install process is finished now!

The next step is to copy your CA certificate from **/opt/etc/openvpn/keys/ca.crt** to local machines.

There are many ways to copy this file. For example, you can copy it using your samba or nfs share, ftp server or other ways.<br>
Note: Do not copy <b>ca.key</b> to any host. You must keep this file in secret!<br>
<br>
And the last step is to add accounts data to <b>/opt/etc/openvpn/secrets</b>.<br>
Each line should contain username and password delimited with spaces or tab symbol.<br>
There are also several ways to edit this file.<br>
<ul><li>You can use some intaractive editor (like <i><b>nano</b></i> or <i><b>vi</b></i>)<br>
</li><li>You can use <i><b>echo</b></i>:<br>
<pre><code># echo "your_user_name	your_secret" &gt;&gt; /opt/etc/openvpn/secrets<br>
</code></pre>
</li><li>Or, for example, you can use <i><b>cat</b></i>:<br>
<pre><code># cat - &gt;&gt; /opt/etc/openvpn/secrets<br>
</code></pre>
<blockquote>(type login and password, then press Enter, and then press CTRL+D)</blockquote></li></ul>

When everything is ready you can start the server:<br>
<pre><code># /opt/etc/init.d/S20openvpn start<br>
</code></pre>

<h2>Configure Client Machine</h2>
You should install openvpn to your client machine. There are many GUI solutions.<br>
For example:<br>
<br>
<ul><li><a href='http://sourceforge.net/projects/ovpnp/files/'>Windows XP / Seven portable</a> version.</li></ul>

<ul><li><a href='http://tunnelblick.googlecode.com'>Here you can find</a> OpenVPN client and instructions for Mac OS.</li></ul>

The common configuration for client is:<br>
<br>
<pre><code>client<br>
remote your_ext_ip_address or domain<br>
ca /path_to/ca.crt<br>
auth-user-pass<br>
cipher AES-128-CBC<br>
comp-lzo yes<br>
dev tap<br>
proto udp<br>
nobind<br>
auth-nocache<br>
script-security 2<br>
persist-key<br>
persist-tun<br>
user openvpn<br>
group openvpn<br>
</code></pre>


<h2>Current Configuration in Details</h2>
The current server configuration is:<br>
<pre><code>## Openvpn configuration file<br>
## /opt/etc/openvpn/openvpn.conf<br>
<br>
#******************************************************************************#<br>
# There are 3 ranges of configuration below. If you want to change your server #<br>
# ip range, you can comment lines in current configuration and uncomment       #<br>
# another section or change it to your own range.                              #<br>
#******************************************************************************#<br>
<br>
#########################################<br>
# config. 1 (current configuration)<br>
#----------------------------------------<br>
ifconfig 10.249.84.1 255.255.255.0<br>
server 10.249.84.0 255.255.255.0<br>
push "route 10.249.84.0 255.255.255.0"<br>
push "dhcp-option DNS 10.249.84.1"<br>
<br>
#########################################<br>
# config. 2<br>
#----------------------------------------<br>
;ifconfig 172.29.167.1 255.255.255.0<br>
;server 172.29.167.0 255.255.255.0<br>
;push "route 172.29.167.0 255.255.255.0"<br>
;push "dhcp-option DNS 172.29.167.1"<br>
<br>
#########################################<br>
# config. 3<br>
#----------------------------------------<br>
;ifconfig 192.168.214.1 255.255.255.0<br>
;server 192.168.214.0 255.255.255.0<br>
;push "route 192.168.214.0 255.255.255.0"<br>
;push "dhcp-option DNS 192.168.214.1"<br>
<br>
<br>
<br>
dev tap<br>
<br>
proto udp<br>
port 1194<br>
<br>
client-to-client<br>
<br>
push "route 224.0.0.0 240.0.0.0"<br>
push "route 192.168.1.1 255.255.255.0"<br>
push "dhcp-option WINS 192.168.1.1"<br>
<br>
up ./openvpn.up<br>
<br>
tls-server<br>
<br>
script-security 2<br>
cipher aes-128-cbc<br>
<br>
ca /opt/etc/openvpn/keys/ca.crt<br>
dh /opt/etc/openvpn/keys/dh1024.pem<br>
cert /opt/etc/openvpn/keys/server.crt<br>
key /opt/etc/openvpn/keys/server.key<br>
<br>
comp-lzo<br>
persist-tun<br>
persist-key<br>
verb 3<br>
<br>
user nobody<br>
group nobody<br>
<br>
keepalive 10 60<br>
</code></pre>
Note: 192.168.1.1 is used as router ip address in this example. If you changed this value it will be also changed in your openvpn configuration file.<br>
<br>
You should bear in mind that there are three ip ranges given for private usage (<a href='http://tools.ietf.org/html/rfc1918'><b>RFC1918</b></a>). They are:<br>
<pre><code> class         range start        range end<br>
----------------------------------------------<br>
class A		10.0.0.0	10.255.255.255<br>
class B		172.16.0.0	172.31.255.255<br>
class C		192.168.0.0	192.168.255.255<br>
</code></pre>

Some ISP provide an access to their local network. You should check that ip addresses of your virtual openvpn network are not used by your ISP. If there are any conflicts, you will not be able to rich local sources of your ISP.<br>
<br>
There are three sections with ip addresses in configuration file above. By default your vpn server will use 10.249.84.1 255.255.255.0. The next two sections are commentes with ';'. This means that they are not used. You can comment the first section and uncomment the second or third section to change the server ip address.<br>
<br>
<pre><code>ifconfig 10.249.84.1 255.255.255.0<br>
server 10.249.84.0 255.255.255.0<br>
</code></pre>
These lines mean that <b>10.249.84.1</b> will be assigned to server. Clients will be assigned with addresses from <b>10.249.84.0</b> network.<br>
Network mask <b>255.255.255.0</b> means that we have 254 useable ip addresses. As we assigned the first one to server 253 ip addresses are available for clients.<br>
<br>
<pre><code>push "route 192.168.1.1 255.255.255.0"<br>
push "route 10.249.84.0 255.255.255.0"<br>
</code></pre>
These routes are sent to client when it connects. Client should know how to reach the server from internet, and also we'd like client could reach any host from home network range.<br>
<br>
<pre><code>push "dhcp-option DNS 10.249.84.1"<br>
</code></pre>
We send to client information to use vpn server as a main dns server. This means, for example, that you'll be able to reach your router's admin interface by typing <b><a href='http://my.router/'>http://my.router/</a></b> in web browser from any place in internet.<br>
<br>
<pre><code>dev tap<br>
</code></pre>
We create create an ethernet tunnel between server and client.<br>
<br>
<pre><code>proto udp<br>
port 1194<br>
</code></pre>
We use default values for these parameters.<br>
<br>
<pre><code>client-to-client<br>
</code></pre>
We want clients to "see" each other. By default clients will only "see" the server.<br>
<br>
<pre><code>up ./openvpn.up<br>
</code></pre>
Shell command to run after successful TUN/TAP device open. The up script is used for specifying route commands which route IP traffic destined for private subnets which exist at the other end of the VPN connection into the tunnel.<br>
<br>
<pre><code>tls-server<br>
</code></pre>
TLS mode is the most powerful crypto mode of OpenVPN in both security and flexibility. TLS mode works by establishing control and data channels which are multiplexed over a single TCP/UDP port.<br>
<br>
<pre><code>script-security 2<br>
</code></pre>
This directive offers policy-level control over OpenVPN's usage of external programs and scripts. Lower level values are more restrictive, higher values are more permissive. This level (2) - allows calling of built-in executables and user-defined scripts.<br>
<br>
<pre><code>cipher aes-128-cbc<br>
</code></pre>
Encrypt packets with cipher algorithm aes-128-cbc.<br>
<br>
<pre><code>ca /opt/etc/openvpn/keys/ca.crt<br>
dh /opt/etc/openvpn/keys/dh1024.pem<br>
cert /opt/etc/openvpn/keys/server.crt<br>
key /opt/etc/openvpn/keys/server.key<br>
</code></pre>
Path to certificates and keys required by server.<br>
<br>
<pre><code>comp-lzo<br>
</code></pre>
Use fast LZO compression. May add up to 1 byte per packet for incompressible data.<br>
<br>
<pre><code>persist-tun<br>
</code></pre>
Don't close and reopen TUN/TAP device or run up/down scripts.<br>
<br>
<pre><code>persist-key<br>
</code></pre>
Don't re-read key files.<br>
<br>
<br>
<pre><code>verb 3<br>
</code></pre>
Set output verbosity to n (default=1). Each level shows all info from the previous levels. Level 3 is recommended if you want a good summary of what's happening without being swamped by output.<br>
<br>
<pre><code>user nobody<br>
group nobody<br>
</code></pre>
By setting user to nobody or somebody similarly unprivileged, the hostile party would be limited in what damage they could cause.<br>
<br>
<pre><code>keepalive 10 60<br>
</code></pre>
Expands as follows:<br>
<pre><code> if mode server:<br>
   ping 10<br>
   ping-restart 120<br>
   push "ping 10"<br>
   push "ping-restart 60"<br>
 else<br>
   ping 10<br>
   ping-restart 60<br>
</code></pre>
It is a helper directive designed to simplify the expression of ping and ping-restart in server mode configurations.<br>
<br>
<br>
<h2>Custom Configuration</h2>
OpenVPN can be configured many different ways to get rich a goal.<br>
<br>
If you need to customise the server configuration you should edit:<br>
<pre><code># nano /opt/etc/openvpn/openvpn.conf<br>
</code></pre>

There are also several examples of configuration available in:<br>
<pre><code># ls -la /opt/etc/openvpn/sample/config-files<br>
</code></pre>

Follow <a href='http://openvpn.net/index.php/open-source/documentation/howto.html'><b>this HowTo</b></a> to get the detailed information.<br>
<br>
<br>
<h2>Generating Certificates and Keys</h2>
If you need to create new certificates, you can use the script:<br>
<pre><code># /opt/etc/openvpn/openvpn-cert.sh<br>
</code></pre>

Or you can generete them yourself using <i><b>openssl</b></i> command.<br>
<br>
<i>The next command will create new root certificate and root key:</i>
<pre><code># openssl req -nodes -days 1095 -x509 -newkey rsa:1024 -outform PEM -out ca.crt<br>
</code></pre>

<i>The next command will create new certificate and key pair:</i>
<pre><code># openssl genrsa -out name.key<br>
<br>
# openssl req -new -nodes -key name.key -out name.csr<br>
<br>
# openssl ca -batch -config openssl.cnf -in name.csr -out name.crt<br>
</code></pre>
<i>Use machine name as a 'name' in this example.</i>

<i>The next command will generate new 1024 bit Diffie-Hellman key:</i>
<pre><code># openssl dhparam -out dh1024.pem 1024<br>
</code></pre>
<i>This operation requires much time. Please be patient.</i>
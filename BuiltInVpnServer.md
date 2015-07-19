

# How To Configure Integrated VPN Server On Routers Asus RT-N56U/RT-N65U #

---


This firmware contains an embedded VPN server that easily enough to configure. You get a number of advantages to using a VPN server, including the safe use of function 'wake-on-lan'.

All easily configured through the <a href='http://my.router/vpnsrv.asp'>WEB-interface</a>

  1. Turn on the "Enable VPN Server?". <br>
<ol><li>Select the VPN Server Protocol. <br>
</li><li>Change the type of encryption. <br>
</li><li>Disable the "Broadcast traffic" (or change it to the required value). <br>     ►  <i>Pass broadcast traffic allows, for example, client devices to access resources using SMB-name of the computer, but the activation of this function has a very high load on the CPU while passing of any local traffic</i> <br>
</li><li>Change "VPN Clients IP Pool". This is the number of clients that can connect to your VPN server simultaneously (in this example - 4). <br>  <img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png' />  <b>IMPORTANT!!!</b> The range of IP addresses for VPN clients can not overlap with DHCP-range LAN. <br>
</li><li>Add user accounts (username, password, and, if necessary, assigned IP-address). <br>     ►  <i>Assigned the fixed IP-address (if specified) must be in the range of a pool of IP addresses for VPN clients from p.5</i></li></ol>

Press 'Apply'.<br>
<br>
<br>
<br>
<img src='http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/vpnsrv-042-en.png' />



That's it! Now you need to configure the clients. Configuration depends on your platform.<br>
<br>
The common settings are:<br>
<pre><code>VPN server: your external ip address or DDNS record name<br>
Enable encryption: yes<br>
Encryption type: the one you've set for the server<br>
Username: login from the list entered in item 6<br>
Password: password from the list entered in item 6<br>
</code></pre>

<a href='http://www.techrepublic.com/blog/smartphones/connect-to-a-pptp-vpn-from-your-android-phone/2145'><b>Here is the example</b></a> of PPTP from Android phone.<br>
First, connect to mobile internet (not using WiFi!!), then try to connect to your VPN server. Type <a href='http://my.router/'>http://my.router/</a> in browser to check if this works.<br>
<br>
<br>
<br>

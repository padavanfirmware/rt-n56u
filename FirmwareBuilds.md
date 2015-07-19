

# What is difference between the versions (full, base, etc.) of Firmware for routers Asus RT-N56U/RT-N65U? #

This firmware exists for routers Asus RT-N56U/RT-N65U/RT-N14U/RT-N11P. There are also several Firmware builds (base, full, etc.). In this section we will consider the differences between the various Firmware builds.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png) The _"nano"_ builds exists at <a href='http://rt-n56u.soulblader.com/files/current/'>Nightly builds</a>.

---



## Firmware builds for router ASUS RT-N56U ##

In this section we will consider the differences between the various Firmware builds for router ASUS RT-N56U.


### RT-N56U\_XXX\_aria ###

**Aria2 build**


> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [х] FAT16/FAT32/exFAT filesystem (FAT16/FAT32 via exFAT driver).
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] FUSE kernel modules.
  * [х] UVC camera kernel modules.
  * [х] NFS kernel modules (NFSv2/3 client/server).
  * [х] IPSET kernel modules.
  * [х] LPR printing daemon.
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).
  * [х] sftp (SSH FTP server).
  * [х] vsftpd (FTP server).
  * [х] samba (SMB server).
  * [х] xupnpd (multicast IPTV->UPnP proxy).
  * [х] openvpn (security VPN client/server).
  * [х] https server for WebUI.


> _included:_
  * [+] aria2 (multi-protocol download manager).
  * [+] openssl binary (allow generate certificates for openvpn/https).


> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] transmission (torrent client).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] CIFS client kernel modules.
  * [-] openssh (BSD SSH client/server).
  * [-] tcpdump utility.
  * [-] parted utility.
  * [-] Stripped debug messages from Samba server.


### RT-N56U\_XXX\_base ###

**Base build**

> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [х] FAT16/FAT32/exFAT filesystem (FAT16/FAT32 via exFAT driver).
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] FUSE kernel modules.
  * [х] UVC camera kernel modules.
  * [х] NFS kernel modules (NFSv2/3 client/server).
  * [х] IPSET kernel modules.
  * [х] LPR printing daemon.
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).
  * [х] sftp (SSH FTP server).
  * [х] vsftpd (FTP server).
  * [х] samba (SMB server).
  * [х] xupnpd (multicast IPTV->UPnP proxy).
  * [х] openvpn (security VPN client/server).
  * [х] https server for WebUI.

> _included:_
  * [+] openssl binary (allow generate certificates for openvpn/https).
  * [+] tcpdump utility.

> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] transmission (torrent client).
  * [-] aria2 (multi-protocol download manager).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] CIFS client kernel modules.
  * [-] openssh (BSD SSH client/server).
  * [-] parted utility.
  * [-] Stripped debug messages from Samba server.


### RT-N56U\_XXX\_dlna ###

**DLNA + Transmission build**

> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [х] FAT16/FAT32/exFAT filesystem (FAT16/FAT32 via exFAT driver).
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] FUSE kernel modules.
  * [х] UVC camera kernel modules.
  * [х] NFS kernel modules (NFSv2/3 client/server).
  * [х] IPSET kernel modules.
  * [х] LPR printing daemon.
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).
  * [х] sftp (SSH FTP server).
  * [х] vsftpd (FTP server).
  * [х] samba (SMB server).
  * [х] xupnpd (multicast IPTV->UPnP proxy).
  * [х] openvpn (security VPN client/server).
  * [х] https server for WebUI.

> _included:_
  * [+] minidlna (UPnP/DLNA A/V mediaserver).
  * [+] transmission (torrent client).

> _excluded:_
  * [-] firefly (iTunes audio mediaserver).
  * [-] aria2 (multi-protocol download manager).
  * [-] transmission web control (advanced WebUI for transmission).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] CIFS client kernel modules.
  * [-] openssh (BSD SSH client/server).
  * [-] openssl binary (allow generate certificates for openvpn/https).
  * [-] tcpdump utility.
  * [-] parted utility.
  * [-] Stripped debug messages from Samba server.


### RT-N56U\_XXX\_trmd ###

**Transmission build**

> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [х] FAT16/FAT32/exFAT filesystem (FAT16/FAT32 via exFAT driver).
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] FUSE kernel modules.
  * [х] UVC camera kernel modules.
  * [х] NFS kernel modules (NFSv2/3 client/server).
  * [х] IPSET kernel modules.
  * [х] LPR printing daemon.
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).
  * [х] sftp (SSH FTP server).
  * [х] vsftpd (FTP server).
  * [х] samba (SMB server).
  * [х] xupnpd (multicast IPTV->UPnP proxy).
  * [х] openvpn (security VPN client/server).
  * [х] https server for WebUI.

> _included:_
  * [+] transmission (torrent client).
  * [+] transmission web control (advanced WebUI for transmission).
  * [+] openssl binary (allow generate certificates for openvpn/https).
  * [+] tcpdump utility.
  * [+] parted utility.

> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] aria2 (multi-protocol download manager).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] CIFS client kernel modules.
  * [-] openssh (BSD SSH client/server).
  * [-] Stripped debug messages from Samba server.


### RT-N56U\_XXX\_nano ###

**Nano build**

> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).

> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] transmission (torrent client).
  * [-] aria2 (multi-protocol download manager).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [-] FAT16/FAT32/exFAT filesystem (FAT16/FAT32 via exFAT driver).
  * [-] FUSE kernel modules.
  * [-] IPSET kernel modules.
  * [-] LPR printing daemon.
  * [-] UVC camera kernel modules.
  * [-] NFS kernel modules (NFSv2/3 client/server).
  * [-] CIFS client kernel modules.
  * [-] openssh (BSD SSH client/server).
  * [-] openssl binary (allow generate certificates for openvpn/https).
  * [-] tcpdump utility.
  * [-] parted utility.
  * [-] sftp (SSH FTP server).
  * [-] vsftpd (FTP server).
  * [-] samba (SMB server).
  * [-] xupnpd (multicast IPTV->UPnP proxy).
  * [-] openvpn (security VPN client/server).
  * [-] https server for WebUI.
  * [-] Stripped debug messages from Samba server.

---



## Firmware builds for router ASUS RT-N65U ##

In this section we will consider the differences between the various Firmware builds for router ASUS RT-N65U.


### RT-N65U\_XXX\_base ###

**Base build**

> _mandatory:_
  * [х] Linux kernel-3.0.101+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [х] FAT16/FAT32/exFAT filesystem.
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] FUSE kernel modules.
  * [х] UVC camera kernel modules.
  * [х] NFS kernel modules (NFSv2/3 client/server).
  * [х] CIFS client kernel modules.
  * [х] IPSET kernel modules.
  * [х] LPR printing daemon.
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).
  * [х] sftp (SSH FTP server).
  * [х] vsftpd (FTP server).
  * [х] samba (SMB server).
  * [х] xupnpd (multicast IPTV->UPnP proxy).
  * [х] openvpn (security VPN client/server).
  * [х] https server for WebUI.

> _included:_
  * [+] openssl binary (allow generate certificates for openvpn/https).
  * [+] tcpdump utility.

> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] transmission (torrent client).
  * [-] aria2 (multi-protocol download manager).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] openssh (BSD SSH client/server).
  * [-] parted utility.
  * [-] Stripped debug messages from Samba server.


### RT-N65U\_XXX\_full ###

**Full build**

> _mandatory:_
  * [х] Linux kernel-3.0.101+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [х] FAT16/FAT32/exFAT filesystem.
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] FUSE kernel modules.
  * [х] UVC camera kernel modules.
  * [х] NFS kernel modules (NFSv2/3 client/server).
  * [х] CIFS client kernel modules.
  * [х] IPSET kernel modules.
  * [х] LPR printing daemon.
  * [х] USB-over-Ethernet printing daemon.
  * [х] openssh (BSD SSH client/server).
  * [х] sftp (SSH FTP server).
  * [х] vsftpd (FTP server).
  * [х] samba (SMB server).
  * [х] xupnpd (multicast IPTV->UPnP proxy).
  * [х] openvpn (security VPN client/server).
  * [х] https server for WebUI.

> _included:_
  * [+] minidlna (UPnP/DLNA A/V mediaserver).
  * [+] firefly (iTunes audio mediaserver).
  * [+] aria2 (multi-protocol download manager).
  * [+] transmission (torrent client).
  * [+] transmission web control (advanced WebUI for transmission).
  * [+] openssl binary (allow generate certificates for openvpn/https).
  * [+] tcpdump utility.
  * [+] parted utility.

> _excluded:_
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] dropbear (SSH client/server).


### RT-N65U\_XXX\_nano ###

**Nano build**

> _mandatory:_
  * [х] Linux kernel-3.0+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).

> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] transmission (torrent client).
  * [-] aria2 (multi-protocol download manager).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [-] FAT16/FAT32/exFAT filesystem (FAT16/FAT32 via exFAT driver).
  * [-] FUSE kernel modules.
  * [-] IPSET kernel modules.
  * [-] LPR printing daemon.
  * [-] UVC camera kernel modules.
  * [-] NFS kernel modules (NFSv2/3 client/server).
  * [-] CIFS client kernel modules.
  * [-] openssh (BSD SSH client/server).
  * [-] openssl binary (allow generate certificates for openvpn/https).
  * [-] tcpdump utility.
  * [-] parted utility.
  * [-] sftp (SSH FTP server).
  * [-] vsftpd (FTP server).
  * [-] samba (SMB server).
  * [-] xupnpd (multicast IPTV->UPnP proxy).
  * [-] openvpn (security VPN client/server).
  * [-] https server for WebUI.
  * [-] Stripped debug messages from Samba server.

---



## Firmware builds for router ASUS RT-N14U ##

In this section we will consider the differences between the various Firmware builds for router ASUS RT-N14U.


### RT-N14U\_XXX\_base ###

**Base build**

> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [х] FAT16/FAT32/exFAT filesystem.
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] FUSE kernel modules.
  * [х] UVC camera kernel modules.
  * [х] NFS kernel modules (NFSv2/3 client/server).
  * [х] CIFS client kernel modules.
  * [х] IPSET kernel modules.
  * [х] LPR printing daemon.
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).
  * [х] sftp (SSH FTP server).
  * [х] vsftpd (FTP server).
  * [х] samba (SMB server).
  * [х] xupnpd (multicast IPTV->UPnP proxy).
  * [х] openvpn (security VPN client/server).
  * [х] https server for WebUI.

> _included:_
  * [+] openssl binary (allow generate certificates for openvpn/https).
  * [+] tcpdump utility.

> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] transmission (torrent client).
  * [-] aria2 (multi-protocol download manager).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] openssh (BSD SSH client/server).
  * [-] parted utility.
  * [-] Stripped debug messages from Samba server.


### RT-N14U\_XXX\_full ###

**Full build**

> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [х] FAT16/FAT32/exFAT filesystem.
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] FUSE kernel modules.
  * [х] UVC camera kernel modules.
  * [х] NFS kernel modules (NFSv2/3 client/server).
  * [х] CIFS client kernel modules.
  * [х] IPSET kernel modules.
  * [х] LPR printing daemon.
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).
  * [х] sftp (SSH FTP server).
  * [х] vsftpd (FTP server).
  * [х] samba (SMB server).
  * [х] xupnpd (multicast IPTV->UPnP proxy).
  * [х] openvpn (security VPN client/server).
  * [х] https server for WebUI.

> _included:_
  * [+] minidlna (UPnP/DLNA A/V mediaserver).
  * [+] firefly (iTunes audio mediaserver).
  * [+] aria2 (multi-protocol download manager).
  * [+] transmission (torrent client).
  * [+] transmission web control (advanced WebUI for transmission).
  * [+] openssl binary (allow generate certificates for openvpn/https).
  * [+] tcpdump utility.
  * [+] parted utility.

> _excluded:_
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] openssh (BSD SSH client/server).


### RT-N14U\_XXX\_nano ###

**Nano build**

> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [х] USB-over-Ethernet printing daemon.
  * [х] dropbear (SSH client/server).

> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] transmission (torrent client).
  * [-] aria2 (multi-protocol download manager).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [-] FAT16/FAT32/exFAT filesystem (FAT16/FAT32 via exFAT driver).
  * [-] FUSE kernel modules.
  * [-] IPSET kernel modules.
  * [-] LPR printing daemon.
  * [-] UVC camera kernel modules.
  * [-] NFS kernel modules (NFSv2/3 client/server).
  * [-] CIFS client kernel modules.
  * [-] openssh (BSD SSH client/server).
  * [-] openssl binary (allow generate certificates for openvpn/https).
  * [-] tcpdump utility.
  * [-] parted utility.
  * [-] sftp (SSH FTP server).
  * [-] vsftpd (FTP server).
  * [-] samba (SMB server).
  * [-] xupnpd (multicast IPTV->UPnP proxy).
  * [-] openvpn (security VPN client/server).
  * [-] https server for WebUI.
  * [-] Stripped debug messages from Samba server.

---



## Firmware builds for router ASUS RT-N11P ##

In this section we will consider the differences between the various Firmware builds for router ASUS RT-N11P.


### RT-N11P\_XXX\_base ###

**Base build**

> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] dropbear (SSH client/server).

> _included:_
  * [+] openssl binary (allow generate certificates for openvpn/https).
  * [+] tcpdump utility.
  * [+] xupnpd (multicast IPTV->UPnP proxy).

> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] transmission (torrent client).
  * [-] aria2 (multi-protocol download manager).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [-] FAT16/FAT32/exFAT filesystem.
  * [-] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [-] FUSE kernel modules.
  * [-] UVC camera kernel modules.
  * [-] NFS kernel modules (NFSv2/3 client/server).
  * [-] CIFS client kernel modules.
  * [-] IPSET kernel modules.
  * [-] LPR printing daemon.
  * [-] USB-over-Ethernet printing daemon.
  * [-] openssh (BSD SSH client/server).
  * [-] sftp (SSH FTP server).
  * [-] vsftpd (FTP server).
  * [-] samba (SMB server).
  * [-] openvpn (security VPN client/server).
  * [-] https server for WebUI.
  * [-] parted utility.
  * [-] Stripped debug messages from Samba server.


### RT-N11P\_XXX\_nano ###

**Nano build**

> _mandatory:_
  * [х] Linux kernel-3.4+ (with upstream backports).
  * [х] IPv6 full support (native and SIT tunnels).
  * [х] dropbear (SSH client/server).

> _excluded:_
  * [-] minidlna (UPnP/DLNA A/V mediaserver).
  * [-] firefly (iTunes audio mediaserver).
  * [-] transmission (torrent client).
  * [-] aria2 (multi-protocol download manager).
  * [-] QoS kernel modules.
  * [-] IFB/IMQ kernel modules.
  * [-] USB HID kernel modules.
  * [-] XFS filesystem.
  * [-] NTFS filesystem (Paragon ufsd 8.6 for ASUS).
  * [-] FAT16/FAT32/exFAT filesystem.
  * [-] EXT4/EXT3/EXT2 filesystem (EXT3/EXT2 via EXT4 driver).
  * [-] FUSE kernel modules.
  * [-] UVC camera kernel modules.
  * [-] NFS kernel modules (NFSv2/3 client/server).
  * [-] CIFS client kernel modules.
  * [-] IPSET kernel modules.
  * [-] LPR printing daemon.
  * [-] USB-over-Ethernet printing daemon.
  * [-] openssh (BSD SSH client/server).
  * [-] sftp (SSH FTP server).
  * [-] vsftpd (FTP server).
  * [-] samba (SMB server).
  * [-] parted utility.
  * [-] Stripped debug messages from Samba server.

---





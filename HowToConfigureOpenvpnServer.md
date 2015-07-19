

# How To Configure Bild-In OpenVPN On Asus RT-N56U/RT-N65U Routers #

---


This firmware contains built-in OpenVPN (see [Firmware Builds](https://rt-n56u.googlecode.com/p/rt-n56u/wiki/FirmwareBuilds)), which can be configured via Web Interface. This HowTo covers questions of certificates creation. Most of users experience problems with this process.

First of all, let's assume that persons, who maintain applications on server and client side are two different people. You should **never** send authentication data in clear (human readable) form. And sensitive authentication data (such as private keys, etc) should not be sent to anybody at all!

Certificates may have different usage purposes, which can be set using certificate extensions. For example, if there is no CA extension in certificate, it can't be used for signature verification of other certificates.

## Each side (both server and client) should have at least ##
  1. Private key.
  1. Certificate, signed by CA.
  1. Diffie–Hellman Key.
## Optional (depends on server settings) ##
  1. TLS Authorization Key



---

## _Files purpose:_ ##
| **Filename** | **Needed By** | **Purpose** | **Secret** |
|:-------------|:--------------|:------------|:-----------|
| ca.crt       | server + all clients | Root CA certificate | NO         |
| ca.key       | key signing machine only | Root CA key | YES        |
| server.crt   | server only   | Server Certificate | NO         |
| server.key   | server only   | Server Key  | YES        |
| client1.crt  | client1 only  | Client1 Certificate | NO         |
| client1.key  | client1 only  | Client1 Key | YES        |
| dh{n}.pem    | server only   | Diffie Hellman parameters | NO         |
| ta.key       | server + all clients | tls-auth HMAC signature | YES        |

## Install Server Side Certificates ##
### Common Algorithm ###
  1. Create CA certificate and private key
  1. Create server private key and certificate, signed by CA
  1. Create Diffie–Hellman Key
  1. Optional: Create TLS Key

Change directory to server certificate storage:
```
# cd /etc/storage/openvpn/server
```

#### Create CA certificate and private key ####
```
# openssl req -nodes -x509 -days 3650 -newkey rsa:2048 -outform PEM -out ca.crt -keyout ca.key -sha1
```
This command creates new RSA private key 1024 bits long (ca.key) and self-signed certificate with 'CA:TRUE' extension (ca.crt) valid for 10 years. We will sign other certificates using private key (ca.key). CA certificate (ca.crt) can be sent to anyone for signature verification.

---

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)_**Note:**_ _Common Name_ field should not be blank!

---

If you don't want fill all fields by hands, you can use:
```
# openssl req -nodes -x509 -days 365 -newkey rsa:2048 -outform PEM -out ca.crt -keyout ca.key -sha1 -subj '/CN=My OpenVPN CA'
```
This certificate will be valid for 1 year (change _-days_ value if needed). Certificate can't be used for its purpose when it is expired. But new caertificate can be generated and signed using the same Key (ca.key). (Keys do not expire.) This can be done with:
```
# openssl req -nodes -x509 -days 365 -new -outform PEM -out ca.crt -key ca.key -sha1 -subj '/CN=My OpenVPN CA'
```

Certificate content can be viewed with:
```
# openssl x509 -text -noout -in ca.crt
```
As far as private key is a secret:
```
# chmod 600 ca.key
```

---

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)_**Note:**_ CA key (ca.key) is required only for CSR (certificate signing request) sign and most of time it not needed. It is very sensitive component. It is recommended to encrypt and/or put it to more secure storage.
```
# openssl rsa -aes256 -in ca.key -out ca.key.aes
# mv ca.key.aes ca.key
# chmod 600 ca.key
```
Password phrase should be 4 to 1024 characters. Next time when you'll sign a certificate this password will be asked.

---


#### Create server certificate ####
Let's create certificate signing request:
```
# openssl req -nodes -days 365 -newkey rsa:2048 -outform PEM -out server.csr -keyout server.key -sha1 -subj '/CN=example.com'
```
This command creates a new private key (server.key) and signing request (server.csr), valid for 1 year.
Let's sign our server certificate with CA:
```
# openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key -CAcreateserial -clrext -out server.crt -sha1
```
We don't need for request any more:
```
# rm -f server.csr
# chmod 600 server.key
```

#### Create Diffie–Hellman Key ####
```
# openssl dhparam -out dh1024.pem 1024
```
This command creates dh1024.pem file, which contains a l\_ooo\_ng prime.

#### Optional: Create TLS Key ####
This key is required if TLS-Auth is set to 'Yes' in server settings.
```
# openvpn --genkey --secret ta.key
# chmod 600 ta.key
```
<a href='Hidden comment: 
FIXME: Not sure about the following
'></a>
_**Note**_: This key should be known by server and client and should not be seen by any other 3rd parties. This key should be copied over a pre-existing secure channel to the server and all client machines.

To save changes to flash-memory on router:
```
# mtd_storage.sh save
```


## Install Client Side Certificates ##
### Common Algorithm ###
  1. Create client certificate signing request and send it to the CA (to server)
  1. Get signed certificate (client.crt), CA (ca.crt) and install them
  1. Optional: Get TLS key over a pre-existing secure channel (depends on server settings)

#### Create client certificate signing request and send it to the CA (to server) ####
Change directory to client certificate storage:
```
# cd /etc/storage/openvpn/client
```

Let's create CSR:
```
# openssl req -nodes -days 365 -newkey rsa:2048 -outform PEM -out client.csr -keyout client.key -sha1 -subj '/CN=client1.example.com'
# chmod 600 client.key
```
This command creates client private key (client.key) and client CSR, which will be valid for 1 year (client.csr) with Common Name = client1.example.com. Common Name is important, for example, if you'd like to access network befind the client.

#### Get signed certificate (client.crt), CA (ca.crt) and install them ####
CA (ca.crt), client certificate (client.crt) and client key (client.key) should be installed:
  * Go to http://my.router/vpncli.asp
  * Turn on VPN client
  * Change VPN protocol to OpenVPN
  * Open 'Certificates and Keys' tap and copy-paste all keys to fields
Other client settings should be set according to server settings.

If TLS Key is encrypted (as written below) decrypt it with:
```
# openssl smime -decrypt -aes-256-cbc -inform PEM -in ta.key.aes -inkey client.key -out ta.key
# chmod 600 ta.key
```

## Add a Client ##
### Common Algorithm ###
  1. Sign CSR from client (client.csr)
  1. Send signed certificate (client.crt), CA certificate (ca.crt) to client
  1. Optional: Send TLS Key (ta.key) over a pre-existing secure channel (depends on server settings)

#### Sign CSR from client (client.csr) ####
View CSR with:
```
# openssl req -text -noout -in client.csr
```

Sign a request:
```
# openssl x509 -req -in client.csr -CA ca.crt -CAkey ca.key -CAcreateserial -clrext -out client.crt -sha1
```
_(-clrext option cleans all extensions, which could be set by client on request generation)_

#### Send signed certificate (client.crt), CA certificate (ca.crt) to client ####
Files can be sent in clear form to client.

If it is required to access local network behind a client, you should add _Common Name_ of this client to _**Username**_ field in _**VPN Clients Accounts**_ on http://my.router/vpnsrv.asp.
![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/openvpn_client_lan-en.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/openvpn_client_lan-en.png)

In the example above client with _Common Name = client1.example.com_ with be assigned with static ip address 192.168.111.23. Also routes will be added to access 172.20.21.0/24.

---

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)_**Note:**_ Access to resources can be restricted by client.

---

#### Optional: Send TLS Key (ta.key) over a pre-existing secure channel (depends on server settings) ####
TLS Key can encrypted with client certificate. Only that client can decrypt it with client.key.
```
# openssl smime -encrypt -aes-256-cbc -in ta.key -outform PEM -out ta.key.aes client.crt
```
Encrypted key (ta.key.aes) can be sent with certificates. Client should be notified with a cipher (aes-256-cbc).

## Creating Certificates Using Script ##
There is the script, which should help you:
```
# openvpn-cert.sh --help
```

## How to Block Connection if one of certificates was compromised ##
It is useful to keep serial numbers of signed client certificates.

Let's create directory, where we will put such certificates:
```
# mkdir /etc/storage/openvpn/server/crl
```
Add the following line to OpenVPN configuration:
```
crl-verify /etc/storage/openvpn/server/crl dir
```
Now we need to create file in this directory. The name of this file should be serial number (in decimal) of compromised certificate.

Let's assume we have a copy of that certificate (or we know its serial number).
```
# openssl x509 -noout -serial -in client.crt
serial=AA1E3C74A9D241D1

# printf '%lu\n' 0xAA1E3C74A9D241D1
12258301707512070609

# touch /etc/storage/openvpn/server/crl/12258301707512070609
```

## Conclusion ##
I'd like to say that OpenVPN provides huge amount of opportunities. Its configuration is very flexible. Please find additional information in [official documentation](http://openvpn.net/index.php/open-source/documentation.html).
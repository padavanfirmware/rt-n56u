

**How To Independently Build Firmware For The Routers ASUS RT-N56U/RT-N65U**

---



Instructions for independently build firmware for your router from source in Ubuntu 13.04 i386.

---


1. Install to your PC the <a href='https://www.virtualbox.org/wiki/Downloads/'>Oracle VirtualBox</a>.

2. Download Ubuntu 13.04 i386 (for example,  <a href='http://old-releases.ubuntu.com/releases/13.04/ubuntu-13.04-desktop-i386.iso'>from this mirror</a>).

3. Create new virtual machine and install Ubuntu from step 2 to it. VirtualBox may use a ISO-image as drive in virtual machine.

![http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png](http://dl.dropboxusercontent.com/u/44733876/googlecode/pic/warning.png)  If you plan to use Ubuntu with the GUI, you must dedicate at least 1.5Gb of RAM for the virtual machine. When you select a smaller size of RAM you may receive errors when you create the image of the firmware.

4. Start your virtual machine and open _Terminal_ on it.

5. Install git:
```
sudo apt-get update 
sudo apt-get install git
```

6. Go to directory /opt and run command for create the local copy of repository:
```
cd /opt
sudo git clone https://code.google.com/p/rt-n56u/
```
This copies all the source code, creates a local git-repository. Directory /opt/rt-n56u will be the root of the git-repository.

7. Read the document /opt/rt-n56u/readme.eng.txt and install all the required packages that are listed in it:
```
sudo apt-get install build-essential gawk pkg-config gettext automake autoconf libtool bison flex zlib1g-dev libgmp3-dev libmpfr-dev libmpc-dev texinfo mc
```
mc (midnight commander) do not need to build the firmware, but it will help you navigate through directories, copy or edit files.

8. Go to directory with toolchain sources (cross-compiler and tools for building) and build it:
```
cd /opt/rt-n56u/toolchain-mipsel
sudo ./clean_sources
sudo ./build_toolchain
```
The result will be collected the target of toolchain /opt/rt-n56u/toolchain-mipsel/toolchain-3.4.x

If you plan to build the firmware with the kernel 3.0, you must build the appropriate version of tolchain:
```
cd /opt/rt-n56u/toolchain-mipsel
sudo ./clean_sources
sudo ./build_toolchain_3.0.x
```
The result will be collected the target of toolchain /opt/rt-n56u/toolchain-mipsel/toolchain-3.0.x

In the future, you will need these commands only if the toolchain will be updated.

9. Now go to directory with sources:
```
cd /opt/rt-n56u/trunk
```
and edit file /opt/rt-n56u/trunk/.config to fit your needs.

Edit path to toolchain (if you need it):
```
CONFIG_TOOLCHAIN_DIR=/opt/rt-n56u/toolchain-mipsel 
```

To build the firmware, for example, for router RT-N65U uncomment (remove the simbol #) the line:
```
CONFIG_FIRMWARE_PRODUCT_ID="RT-N65U"
```
and comment the line:
```
CONFIG_FIRMWARE_PRODUCT_ID="RT-N56U"
```

Save the file after edit.

10. Clear source tree (every time before a new build)
```
sudo ./clear_tree
```

11. Build the firmware:
```
sudo ./build_firmware
```
Created custom firmware file will be in the directory ./path\_to\_your\_dir/rt-n56u/trunk/images. If you want to save the firmware that you created earlier - copy it to another location, because the command clear\_tree overwrites the directory images.

12. When <a href='http://code.google.com/p/rt-n56u/source/list'>repository</a> updated a local source tree must be updated with command:
```
sudo git pull
```

13. If you made ​​any changes to the local repository, when you upgrade tree some files could not be copied. In this case, you must give the command:
```
sudo git stash
sudo git pull
```

14. If toolchain sources (cross-compiler and tools for building) is changed you must re-build it:
```
cd /opt/rt-n56u/toolchain-mipsel
sudo ./clean_sources  
sudo ./clean_toolchain  
sudo ./build_toolchain 
```



---

Main Author: **Return from Hell**

---



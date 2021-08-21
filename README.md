# BANANAPI
Write SD CARD boot System Linux in board BananaPi, updates, softwares, configurations services network, etc

![img0.png](http://www.lemaker.org/Public/uploads/product/2015/1022/56284d9b0d292_thumb.jpg)

> Manual PDF
http://mirror.lemaker.org/Banana%20Pro%20&%20Pi%20User%20Manual-V1.0.pdf

> Download image Raspbian For BananaPro V1412

![img0.png](http://www.lemaker.org/Public/uploads/file/2015/1020/5625a399abfe4.png)

http://www.lemaker.org/product-bananapro-download-16.html or https://drive.google.com/file/d/0B38hUt6ypQXDRDNZek54MncxWWM/view?usp=sharing

# INSTALL IMAGE RASPBIAN IN TO SD CARD

> On Linux
```
sudo fdisk -l
sudo dd if=/media/images/Raspbian_For_BananaPro_v1412.img of=/dev/sdb bs=1M && syn

```
> On Windows 10
Download https://sourceforge.net/projects/win32diskimager/

![img0.png](https://a.fsdn.com/con/app/proj/win32diskimager/screenshots/Win32DiskImager-1.0.png/max/max/1)

# Config wifi
> Wifi 

http://wiki.lemaker.org/BananaPro/Pi:WiFi_configuration

```
sudo ifconfig
```

if not show `wlan0` execute command in terminal:
```
sudo modprobe ap6210
```
Or edit file `/etc/modules` and insert line `ap6210`


> Edit Wifi config in `cat /etc/wpa_supplicant/wpa_supplicant.conf` and add your access.
```
network={
        ssid="Mozilla"
        psk="yourpasswd"
        proto=RSN
        key_mgmt=WPA-PSK
        pairwise=CCMP
        auth_alg=OPEN
}
```

# Update packages
> update with command in terminal
```
sudo apt-get update
```
> If fail update with message `Err http://mirrordirector.raspbian.org wheezy/rpi armhf Packages`:
```
sudo nano /etc/apt/sources.list
```
> Replace `mirrordirector` to `legacy`
```
deb http://mirrordirector.raspbian.org/raspbian/ wheezy main contrib non-free rpi
```
```
deb http://legacy.raspbian.org/raspbian/ wheezy main contrib non-free rpi
```
> In sequence install packages basics
```
sudo apt-get update -y
sudo apt-get install -y mc
sudo apt-get install -y samba
sudo apt-get install -y samba-common-bin
apt-get install -y tightvncserver
apt-get install -y python-pip
```

# Config SAMBA

Share folders and files in to the network with workstations windows.

> Make folder `public` in to the user space.
```
mkdir /home/bananapi/public
```
> Set permission on folder.
```
chown -R bananapi /home/bananapi/public
chgrp -R pi /home/bananapi/public
```
> Set password for user `bananapi`.
```
smbpasswd -a bananapi
```
> Backup default config SAMBA.
```
mv /etc/samba/smb.conf /etc/samba/smb.conf.bkp
```
> Edit config `nano /etc/samba/smb.conf`, insert content and save.
```
[public]
    path = /home/bananapi/public
    valid users = bananapi
    browsable = yes
    writable = yes
    guest ok = yes
    read only = no
    directory mask = 0777
    create mask = 0777
```
> Restart service SAMBA.
```
service samba stop
service samba start
```

> How to enable SMB1 on Windows 10

If you try to access an SMB 1 share from Windows 10 you may receive the following error message:
"You can’t connect to the file share because it’s not secure. This share requires the obsolete SMB1 protocol, which is unsafe and could expose your system to attack. Your system requires SMB2 or higher."

![img0.png](https://www.tachytelic.net/wp-content/uploads/SMB.png)

Enable SMB1 on Windows 10

- Press Windows Key + R to bring up the run dialog and type: `optionalfeatures`.
- Expand “SMB 1.0/CIFS File Sharing Support” and then check the box next to “SMB 1.0/CIFS Client”.
- Click OK.
- The installation will now proceed and you should be able to access shares using the SMB 1 Protocol again.

> Enable SMB1 on Windows 10 with PowerShell

If you would prefer to do a command line installation, use the following command from an elevated PowerShell Prompt:

```
Enable-WindowsOptionalFeature -Online -FeatureName "SMB1Protocol-Client" -All
```

For more information see:
https://support.microsoft.com/en-gb/help/4034314/smbv1-is-not-installed-by-default-in-windows

Reference: https://www.tachytelic.net/2019/09/windows-10-enable-smb1/





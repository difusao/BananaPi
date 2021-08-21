## Config SAMBA

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

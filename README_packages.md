## Update packages

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

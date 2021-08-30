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

# Sessions config

> Wifi
- [x] [README_wifi.md](README_wifi.md)

> Packages
- [x] [README_packages.md](README_packages.md)

> SAMBA Server
- [x] [README_samba.md](README_samba.md)

> Tightvncserver
- [x] [README_tightvncserver.md](README_tightvncserver.md)

> Javascript (NodeJS)
- [x] [README_javascript.md](README_javascript.md)

> DHCP Server
- [ ] [README_dhcpd.md](README_dhcpd.md)

> DNS Server
- [ ] [README_find.md](README_find.md)

> Firewall
- [ ] [README_firewall.md](README_firewall.md)

> PiHole
- [ ] [README_pihole.md](README_pihole.md)



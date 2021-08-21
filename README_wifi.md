## Config wifi and Network
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
        ssid="WifiName"
        psk="WifiPassword"
        proto=RSN
        key_mgmt=WPA-PSK
        pairwise=CCMP
        auth_alg=OPEN
}
```
> Wifi with address IP fixed
Edit file `/etc/network/interfaces`
DHCP
```
auto lo

iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf

iface default inet dhcp
```
IP FIXED
```

```

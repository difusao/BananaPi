## Config wifi Network and ethernet adapter
> Wifi configuration wiki.

http://wiki.lemaker.org/BananaPro/Pi:WiFi_configuration

```
sudo ifconfig
```
if not show `wlan0` execute command in terminal:
```
sudo modprobe ap6210
```
Edit file `/etc/modules` and insert line `ap6210`.
Test wifi connect running `iwconfig`.
```
lo        no wireless extensions.

tunl0     no wireless extensions.

wlan0     IEEE 802.11  ESSID:"Mozilla"
          Mode:Managed  Frequency:2.462 GHz  Access Point: XX:XX:XX:XX:2C:F0
          Bit Rate=26 Mb/s   Tx-Power:32 dBm
          Retry min limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off
          Link Quality=2/5  Signal level=-72 dBm  Noise level=-92 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

eth0      no wireless extensions.
```

> Edit Wifi config in `cat /etc/wpa_supplicant/wpa_supplicant.conf` and add your access.
```
network={
        ssid="Mozilla"
        psk="WifiPassword"
        proto=RSN
        key_mgmt=WPA-PSK
        pairwise=CCMP
        auth_alg=OPEN
        id_str="Mozilla_static"
}
```
> Wifi with address IP fixed
Edit file `/etc/network/interfaces`

IP DYNAMIC (DHCP)
```
auto lo

iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf

iface default inet dhcp
```
IP STATIC
```
auto lo

iface lo inet loopback

allow-hotplug eth0
iface eth0 inet static
address 192.168.2.121
netmask 255.255.255.0
gateway 192.168.2.1

allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf

iface Mozilla_static inet static
address 192.168.2.120
network 255.255.255.0
gateway 192.168.2.1
```

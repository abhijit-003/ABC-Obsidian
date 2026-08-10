```
lsusb   # This will list the divice if connected via a usb

```
https://www.aircrack-ng.org/documentation.html
### Ethernet (USB) not detected
┌──(abhijit㉿Abhi003)-[~]
└─$ cat /etc/NetworkManager/NetworkManager.conf

[main]
plugins=ifupdown,keyfile

[ifupdown]
managed=false

the value `ifupdown` will define whether network manager should consider any ethernet type or not 
- false : Do not consider any ethernet device, this will not detect any ethernet device
---

sudo airmon-ng start wlan0
### 1️⃣ Identify your wireless interface

`iw dev`
### 2️⃣ Enable monitor mode

`sudo airmon-ng start wlan0`
### 3️⃣ Scan surrounding Wi-Fi networks

`sudo airodump-ng wlan0mon`

You’ll see details such as:

- **BSSID** (AP MAC)
    
- **CH** (channel)
    
- **ENC** (WPA2 / WPA3 / OPN)
    
- **ESSID** (Wi-Fi name)
    
- **Signal strength**
    

👉 This is **read-only scanning**, no connection or intrusion.

## Step 1: List all network interfaces

Run:

`ip link show`

Look for names like:

- `wlan0`
    
- `wlp2s0`
    
- `wlan1`
    
- `wlx<MAC>`
    
- `mon0`
  


# OpenWRT Setup and Passwall Installation Guide

## 1. Initial Settings

### Configuring IP Address, WiFi, and Password

1. **Access the OpenWRT Web Interface**: 
   - Connect your computer to the OpenWRT router either via Ethernet cable or via default WiFi.
   - Open a web browser and navigate to `http://192.168.1.1`.

2. **Login**:
   - Enter the default username (`root`) and password (`admin`) to log in.

3. **Change IP Address**:
   - Navigate to `Network` -> `Interfaces`.
   - Click `Edit` on the `LAN` interface.
   - Change the `IPv4 address` to your desired IP address.
   - Click `Save` and `Save & Apply`.

4. **Configure WiFi**:
   - Navigate to `Network` -> `Wireless`.
   - Click `Edit` on the `OpenWrt` network.
   - Set the `ESSID` (WiFi name) and configure the `Wireless Security` settings, including setting a password.
   - Click `Save` and `Save & Apply`.

5. **Change Router Password**:
   - Navigate to `System` -> `Administration`.
   - Under the `Router Password` section, enter your new password.
   - Click `Save & Apply`.

## 2. Install Passwall

### SSH into the Router

1. Open your terminal (or SSH client) and connect to the router:
   ```sh
   ssh root@192.168.1.1

2. Update the package list:
   ```sh
   opkg update

3. Remove the default dnsmasq:
   ```sh
   opkg remove dnsmasq

4. Install dnsmasq-full and required kernel modules:
   ```sh
   opkg install dnsmasq-full
   opkg install kmod-nft-tproxy kmod-nft-socket
   
5. Download and add the Passwall public key:
   ```sh
   opkg install dnsmasq-full
   opkg install kmod-nft-tproxy kmod-nft-socket

6. Download and add the Passwall public key:
   ```sh
   wget -O passwall.pub https://master.dl.sourceforge.net/project/openwrt-passwall-build/passwall.pub
   opkg-key add passwall.pub

7. Set up custom feeds for Passwall:
   ```sh
   read release arch << EOF
$(. /etc/openwrt_release ; echo ${DISTRIB_RELEASE%.*} $DISTRIB_ARCH)
EOF

for feed in passwall_packages passwall2; do
  echo "src/gz $feed https://master.dl.sourceforge.net/project/openwrt-passwall-build/releases/packages-$release/$arch/$feed" >> /etc/opkg/customfeeds.conf
done

8. Update the package list again to include Passwall feeds:
   ```sh
   opkg update

9. Install luci-app-passwall2 and v2ray-geosite-ir:
   ```sh
   opkg install luci-app-passwall2 v2ray-geosite-ir

   

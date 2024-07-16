# OpenWRT Setup and Passwall Installation Guide
[فارسی](https://github.com/Ramtiiin/iran-ip/blob/main/README.fa.md)

## 1. Initial Settings

### Configuring IP Address, WiFi, and Password

Read more about [OpenWrt initial settings](https://github.com/Ramtiiin/Install-PassWall-OpenWrt/blob/main/Openwrt-initial-setting.md).

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
```

8. Update the package list again to include Passwall feeds:
   ```sh
   opkg update

9. Install luci-app-passwall2 and v2ray-geosite-ir:
   ```sh
   opkg install luci-app-passwall2 v2ray-geosite-ir

   

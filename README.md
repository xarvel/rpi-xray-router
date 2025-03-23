# rpi-xray-router

https://firmware-selector.openwrt.org/?version=SNAPSHOT&target=bcm27xx%2Fbcm2712&id=rpi-5

##### Installed Packages
```
... luci nano xray-core v2ray-geoip v2ray-geosite kmod-mt76x2u usbutils kmod-usb2 kmod-usb3 kmod-nft-tproxy kmod-mt7921u
```

##### Script to run on first boot (uci-defaults)
```
uci set wireless.radio0.disabled=0
uci commit wireless

uci delete network.lan
uci delete network.wan
uci delete network.@device[0]
uci delete network.@device[1]

# Configure Bridge Device
uci add network device
uci set network.@device[-1]="device"
uci set network.@device[-1].name="br-lan"
uci set network.@device[-1].type="bridge"

# Configure LAN Interface
uci set network.lan="interface"
uci set network.lan.device="br-lan"
uci set network.lan.proto="static"
uci set network.lan.ipaddr="192.168.4.1"
uci set network.lan.netmask="255.255.255.0"

# Configure WAN Interface
uci set network.wan="interface"
uci set network.wan.proto="dhcp"
uci set network.wan.device="eth0"

# Configure Ethernet Device
uci add network device
uci set network.@device[-1]="device"
uci set network.@device[-1].name="eth0"
uci set network.@device[-1].ipv6="1"

uci commit network

uci set xray.enabled.enabled=1
uci commit xray
```


Commons# show run
version 6.5.4.0-6.5.4
virtual-controller-country DE
virtual-controller-key cf8c8b5f011f9b6db90089b259b174ed7c6a40e34fd0f33dfe
name SetMeUp-C3:74:00
terminal-access
clock timezone none 00 00
rf-band all

allow-new-aps
allowed-ap 34:fc:b9:c3:74:00
allowed-ap 34:fc:b9:c3:69:e4
allowed-ap 34:fc:b9:c3:80:02
allowed-ap 34:fc:b9:c3:7e:5c
allowed-ap c8:b5:ad:c1:4f:66
allowed-ap 34:fc:b9:c3:7e:a6
allowed-ap 34:fc:b9:c3:80:0c
allowed-ap 34:fc:b9:c3:6a:ba



arm
 wide-bands 5ghz
 80mhz-support
 min-tx-power 18
 max-tx-power 127
 band-steering-mode prefer-5ghz
 air-time-fairness-mode default-access
 client-aware
 scanning


syslog-level warn ap-debug
syslog-level warn network
syslog-level warn security
syslog-level warn system
syslog-level warn user
syslog-level warn user-debug
syslog-level warn wireless


extended-ssid





hash-mgmt-password
hash-mgmt-user admin password hash ceb5778d02e6763ed25f1da4e70ac806973527904c38d27c9a6ba7da0031e72fe4afd62821



dpi-error-page-url 0 https://10.0.0.1:8002
dpi-error-page-url 1 http://10.0.0.1:8002
dpi-error-page-url 2 http://172.16.1.1:8002

wlan access-rule stemlab24
 index 0
 rule any any match any any any permit

wlan access-rule default_wired_port_profile
 index 1
 rule any any match any any any permit

wlan access-rule wired-SetMeUp
 index 2
 rule masterip 0.0.0.0 match tcp 80 80 permit
 rule masterip 0.0.0.0 match tcp 4343 4343 permit
 rule any any match udp 67 68 permit
 rule any any match udp 53 53 permit

wlan access-rule SillyNet
 index 3
 rule any any match any any any permit

wlan access-rule "Stemlab Cafe"
 index 4
 rule any any match any any any permit

wlan ssid-profile stemlab24
 enable
 index 0
 type employee
 essid stemlab24
 wpa-passphrase b92400bb911582672e8d445125895b4faf3d8d9a6bfe1596
 opmode wpa2-psk-aes
 max-authentication-failures 0
 vlan 100
 rf-band all
 captive-portal disable
 hide-ssid
 dtim-period 1
 broadcast-filter arp
 dmo-channel-utilization-threshold 90
 local-probe-req-thresh 0
 max-clients-threshold 64
 dot11k

wlan ssid-profile SillyNet
 enable
 index 1
 type employee
 essid SillyNet
 wpa-passphrase 8e62f41b5c30ba2ca21c7da16151f5a69244bb060f72007b
 opmode wpa2-psk-aes
 max-authentication-failures 0
 vlan 1
 rf-band all
 captive-portal disable
 dtim-period 1
 broadcast-filter arp
 dmo-channel-utilization-threshold 90
 local-probe-req-thresh 0
 max-clients-threshold 64
 dot11k

wlan ssid-profile "Stemlab Cafe"
 enable
 index 2
 type employee
 essid "Stemlab Cafe"
 opmode opensystem
 max-authentication-failures 0
 vlan 10
 rf-band all
 captive-portal disable
 dtim-period 1
 broadcast-filter arp
 dmo-channel-utilization-threshold 90
 local-probe-req-thresh 0
 max-clients-threshold 64
 dot11k

auth-survivability cache-time-out 24



wlan external-captive-portal
 server 172.16.1.1:8002
 port 8002
 url "http://172.16.1.1:8002/"
 auth-text ""
 server-fail-through
 auto-whitelist-disable


blacklist-time 3600
auth-failure-blacklist-time 3600

ids
 wireless-containment none


wired-port-profile wired-SetMeUp
 switchport-mode access
 allowed-vlan all
 native-vlan guest
 no shutdown
 access-rule-name wired-SetMeUp
 speed auto
 duplex auto
 no poe
 type guest
 captive-portal disable
 no dot1x

wired-port-profile default_wired_port_profile
 switchport-mode trunk
 allowed-vlan all
 native-vlan 1
 shutdown
 access-rule-name default_wired_port_profile
 speed auto
 duplex full
 no poe
 type employee
 captive-portal disable
 no dot1x


enet0-port-profile default_wired_port_profile

uplink
 preemption
 enforce none
 failover-internet-pkt-lost-cnt 10
 failover-internet-pkt-send-freq 30
 failover-vpn-timeout 180


airgroup
 disable

airgroupservice airplay
 disable
 description AirPlay

airgroupservice airprint
 disable
 description AirPrint




cluster-security
 allow-low-assurance-devices

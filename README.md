enable

copy running-config disk0:/backup-before-transparent.cfg

configure terminal
firewall transparent
hostname asa-transparent

interface GigabitEthernet1/1
 no shutdown
 nameif outside
 security-level 0
 bridge-group 1

interface GigabitEthernet1/2
 no shutdown
 nameif inside
 security-level 100
 bridge-group 1

interface BVI1
 ip address 192.168.88.254 255.255.255.0

interface GigabitEthernet1/1.20
 vlan 20
 no shutdown
 nameif outside_v20
 security-level 0
 bridge-group 20

interface GigabitEthernet1/2.20
 vlan 20
 no shutdown
 nameif inside_v20
 security-level 100
 bridge-group 20

interface BVI20
 ip address 172.22.20.2 255.255.255.0

interface GigabitEthernet1/1.30
 vlan 30
 no shutdown
 nameif outside_v30
 security-level 0
 bridge-group 30

interface GigabitEthernet1/2.30
 vlan 30
 no shutdown
 nameif inside_v30
 security-level 100
 bridge-group 30

interface BVI30
 ip address 172.22.30.2 255.255.255.0

interface GigabitEthernet1/1.50
 vlan 50
 no shutdown
 nameif outside_v50
 security-level 0
 bridge-group 50

interface GigabitEthernet1/2.50
 vlan 50
 no shutdown
 nameif inside_v50
 security-level 100
 bridge-group 50

interface BVI50
 ip address 172.22.50.2 255.255.255.0

interface GigabitEthernet1/1.99
 vlan 99
 no shutdown
 nameif outside_v99
 security-level 0
 bridge-group 99

interface GigabitEthernet1/2.99
 vlan 99
 no shutdown
 nameif inside_v99
 security-level 100
 bridge-group 99

interface BVI99
 ip address 172.22.99.2 255.255.255.0

http server enable
http 192.168.88.0 255.255.255.0 inside
http 172.22.99.0 255.255.255.0 inside_v99

icmp permit 192.168.88.0 255.255.255.0 inside
icmp permit 172.22.99.0 255.255.255.0 inside_v99

route outside 0.0.0.0 0.0.0.0 192.168.88.1

end

write memory
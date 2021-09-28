
```console
enable
conf terminal
hostname <name>
Sw-Floor-1(config)# interface vlan 1
Sw-Floor-1(config-if)# ip address 192.168.1.20 255.255.255.0
Sw-Floor-1(config-if)# no shutdown            # <<< enable interface

# secure user EXEC mode access
configure terminal
line console 0
password cisco
login
end

# secure privileged EXEC access
configure terminal
enable secret class
exit

# check device MAC address
show interface F0/1

# display switch MAC address table
enable
show mac address-table

# clear MAC address table
enable
clear mac address-table dynamic

# ping devices on the network
arp -a


end
```


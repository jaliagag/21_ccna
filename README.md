# CCN cisco course

21-8-2021

1.05, 1.5.7, 2.5.5, 2.7.6, 2.9.1, 2.9.2 ,3.5.5,3.7.9 y 3.7.10

The term network architecture refers to the technologies that support the infrastructure and the programmed services and rules, or protocols, that move data across the network.

4 basic characteristics:

- Fault Tolerance

A fault tolerant network is one that limits the number of affected devices during a failure. It is built to allow quick recovery when such a failure occurs. These networks depend on multiple paths between the source and destination of a message. If one path fails, the messages are instantly sent over a different link. Having multiple paths to a destination is known as redundancy.

Implementing a packet-switched network is one way that reliable networks provide redundancy. Packet switching splits traffic into packets that are routed over a shared network. A single message, such as an email or a video stream, is broken into multiple message blocks, called packets. Each packet has the necessary addressing information of the source and destination of the message. The routers within the network switch the packets based on the condition of the network at that moment. This means that all the packets in a single message could take very different paths to the same destination. In the figure, the user is unaware and unaffected by the router that is dynamically changing the route when a link fails.

- Scalability
- Quality of Service (QoS): managing congestion and ensuring reliable delivery of content to all users.

Congestion occurs when the demand for bandwidth exceeds the amount available. Network bandwidth is measured in the number of bits that can be transmitted in a single second, or bits per second (bps). When simultaneous communications are attempted across the network, the demand for network bandwidth can exceed its availability, creating network congestion.

When the volume of traffic is greater than what can be transported across the network, devices will hold the packets in memory until resources become available to transmit them. The focus of QoS is to prioritize time-sensitive traffic. The type of traffic, not the content of the traffic, is what is important.

QoS, managed by the router, ensures that priorities are matched with the _type of communication_ and its importance to the org. web pages lower priority - VoIP higher priority

- Security

Network administrators must also protect the information contained within the packets being transmitted over the network, and the information stored on network attached devices. In order to achieve the goals of network security, there are three primary requirements.

Confidentiality - Data confidentiality means that only the intended and authorized recipients can access and read data.
Integrity - Data integrity assures users that the information has not been altered in transmission, from origin to destination.
Availability - Data availability assures users of timely and reliable access to data services for authorized users.

There are several networking trends that affect organizations and consumers:

- Bring Your Own Device (BYOD) - BYOD means any device, with any ownership, used anywhere.
- Online collaboration
- Video communications
- Cloud Computing

IOS modes

- User EXEC: view only mode `>`
- Privileged EXEC : super user `#`
  - global configuration mode `<deviceName>(config)#`
    - line config mode: to fconfigure console, ssh, telnet or aux access `switch(config-line)#`
    - interface config mode: configure a switch port or router network interface `switch(config-if)#`

```console
enable              # switch to privileged mode
disable             # return to user exec view only mode
configure terminal  # switch to global config mode
interface vlan 1    # switch to config-if
end                 # or ctrl+z to move from any subconfiguration mode to privileged
```

| Keystroke	| Description |
| ---- | ---- |
|Tab	|Completes a partial command name entry.|
|Backspace|	Erases the character to the left of the cursor.|
|Ctrl+D|	Erases the character at the cursor.|
|Ctrl+K|	Erases all characters from the cursor to the end of the command line.|
|Esc D|	Erases all characters from the cursor to the end of the word.|
|Ctrl+U| or Ctrl+X	Erases all characters from the cursor back to the beginning of the command line.|
|Ctrl+W|	Erases the word to the left of the cursor.|
|Ctrl+A	|Moves the cursor to the beginning of the line.|
|Left Arrowor Ctrl+B|	Moves the cursor one character to the left.|
|Esc B|	Moves the cursor back one word to the left.|
|Esc F|	Moves the cursor forward one word to the right.|
|Right |Arrowor Ctrl+F	Moves the cursor one character to the right.|
|Ctrl+E	|Moves the cursor to the end of command line.|
|Up Arrowor Ctrl+P|	Recalls the previous command in the history buffer, beginning with the most recent command.|
|Down Arrowor Ctrl+N|	Goes to the next line in the the history buffer.|
| Ctrl+R or Ctrl+I or Ctrl+L | Redisplays the system prompt and command line after a console message is received.|


What is the prompt displayed on the screen?
Which command begins with the letter ‘C’?
Which commands are displayed?

```console
S1>
S1>c?
connect
S1>t?
telnet  terminal  traceroute
S1>te?
telnet  terminal
S1>enable
S1#conf t
S1(config)#
```

#### Changing device name

```console
Switch# configure terminal
Switch(config)# hostname Sw-Floor-1
Sw-Floor-1(config)#
```

To return the switch to the default prompt, use the no hostname global config command.

#### password

When you initially connect to a device, you are in user EXEC mode. This mode is secured using the console.

To secure user EXEC mode access, enter line console configuration mode using the line console 0 global configuration command. The zero is used to represent the first (and in most cases the only) console interface. Next, specify the user EXEC mode password using the password password command. Finally, enable user EXEC access using the login command.

```console
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# line console 0
Sw-Floor-1(config-line)# password cisco
Sw-Floor-1(config-line)# login
Sw-Floor-1(config-line)# end
Sw-Floor-1#
```

Console access will now require a password before allowing access to the user EXEC mode.

To secure privileged EXEC access, use the enable secret password global config command, as shown in the example.

```console
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# enable secret class
Sw-Floor-1(config)# exit
Sw-Floor-1#
```

Virtual terminal (VTY) lines enable remote access using Telnet or SSH to the device. Many Cisco switches support up to 16 VTY lines that are numbered 0 to 15.

To secure VTY lines, enter line VTY mode using the line vty 0 15 global config command. Next, specify the VTY password using the password password command. Lastly, enable VTY access using the login command.

```console
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# line vty 0 15
Sw-Floor-1(config-line)# password cisco 
Sw-Floor-1(config-line)# login 
Sw-Floor-1(config-line)# end
Sw-Floor-1#
```

To encrypt all plaintext passwords, use the service password-encryption global config command.

```console
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# service password-encryption
Sw-Floor-1(config)#
```

The command applies weak encryption to all unencrypted passwords. This encryption applies only to passwords in the configuration file, not to passwords as they are sent over the network. The purpose of this command is to keep unauthorized individuals from viewing passwords in the configuration file.

Use the show running-config command to verify that passwords are now encrypted.

```console
Sw-Floor-1(config)# end
Sw-Floor-1# show running-config
!
(Output omitted)
!
line con 0
password 7 094F471A1A0A
login
!
line vty 0 4
 password 7 094F471A1A0A
 login
line vty 5 15
 password 7 094F471A1A0A
 login
!
!
end
```

#### motd

To create a banner message of the day on a network device, use the banner motd # the message of the day # global config command. The “#” in the command syntax is called the delimiting character. It is entered before and after the message. The delimiting character can be any character as long as it does not occur in the message. For this reason, symbols such as the "#" are often used. After the command is executed, the banner will be displayed on all subsequent attempts to access the device until the banner is removed.

```console
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# banner motd #Authorized Access Only#
```

#### exercise

```console
Enter global configuration mode.

Switch#configure terminal
Name the switch “Sw-Floor-1”.

Switch(config)#hostname Sw-Floor-1
Secure user EXEC mode access by entering line console 0, assign the password cisco, enable login, and return to the global configuration mode using exit.

Sw-Floor-1(config)#line console 0
Sw-Floor-1(config-line)#password cisco
Sw-Floor-1(config-line)#login
Sw-Floor-1(config-line)#exit
Secure privileged EXEC mode access using the password class.

Sw-Floor-1(config)#enable secret class
Secure the VTY lines 0 through 15, assign the password cisco, enable login, and return to the global configuration mode using exit.

Sw-Floor-1(config)#line vty 0 15
Sw-Floor-1(config-line)#password cisco
Sw-Floor-1(config-line)#login
Sw-Floor-1(config-line)#exit
Encrypt all plaintext passwords.

Sw-Floor-1(config)#service password-encryption
Create a banner message using the “#” symbol as the delimiter. The banner should display exactly: Warning! Authorized access only!

Sw-Floor-1(config)#banner motd #Warning! Authorized access only!#
You successfully completed the basic requirements to access and secure a device.
```

There are two system files that store the device configuration:

- startup-config - This is the saved configuration file that is stored in NVRAM. It contains all the commands that will be used by the device upon startup or reboot. Flash does not lose its contents when the device is powered off.
- running-config - This is stored in Random Access Memory (RAM). It reflects the current configuration. Modifying a running configuration affects the operation of a Cisco device immediately. RAM is volatile memory. It loses all of its content when the device is powered off or restarted.

To save changes made to the running configuration to the startup configuration file, use the `copy running-config startup-config` or `copy run start` privileged EXEC mode command.

If changes made to the running config do not have the desired effect and the running-config has not yet been saved, you can restore the device to its previous configuration. Remove the changed commands individually, or reload the device using the reload privileged EXEC mode command to restore the startup-config.

The downside to using the reload command to remove an unsaved running config is the brief amount of time the device will be offline, causing network downtime.

When a reload is initiated, the IOS will detect that the running config has changes that were not saved to the startup configuration. A prompt will appear to ask whether to save the changes. To discard the changes, enter n or no.

Alternatively, if undesired changes were saved to the startup config, it may be necessary to clear all the configurations. This requires erasing the startup config and restarting the device. The startup config is removed by using the erase startup-config privileged EXEC mode command. After the command is issued, the switch will prompt you for confirmation. Press Enter to accept.

After removing the startup config from NVRAM, reload the device to remove the current running config file from RAM. On reload, a switch will load the default startup config that originally shipped with the device.

```console
S1#dir ?
  flash:  Directory or file name
  nvram:  Directory or file name 
S1#dir nvram:
```

both flash and nvram are _non_ volatile. the flash memory holds the IOS and nvram holds config file.

- erase configuration: `erase startup-config`
- go to last saved state: `copy startup-config running-config`

The enable password should be replaced with the newer encrypted secret password using the enable secret command. Set the enable secret password to itsasecret.

```console
S1# config t
S1(config)# enable secret itsasecret
S1(config)# exit
S1#
```

Note: The enable secret password overrides the enable password. If both are configured on the switch, you must enter the enable secret password to enter privileged EXEC mode.

## ports and addresses

The use of IP addresses is the primary means of enabling devices to locate one another and establish end-to-end communication on the internet. Each end device on a network must be configured with an IP address.

With the IPv4 address, a subnet mask is also necessary. An IPv4 subnet mask is a 32-bit value that differentiates the network portion of the address from the host portion. Coupled with the IPv4 address, the subnet mask determines to which subnet the device is a member.

The example in the figure displays the IPv4 address (192.168.1.10), subnet mask (255.255.255.0), and default gateway (192.168.1.1) assigned to a host. The default gateway address is the IP address of the router that the host will use to access remote networks, including the internet.

IPv6 addresses are 128 bits in length and written as a string of hexadecimal values. Every four bits is represented by a single hexadecimal digit; for a total of 32 hexadecimal values. Groups of four hexadecimal digits are separated by a colon (:) . IPv6 addresses are not case-sensitive and can be written in either lowercase or uppercase.

Cisco IOS Layer 2 switches have physical ports for devices to connect. These ports do not support Layer 3 IP addresses. Therefore, switches have one or more switch virtual interfaces (SVIs). These are virtual interfaces because there is no physical hardware on the device associated with it. An SVI is created in software.

The virtual interface lets you remotely manage a switch over a network using IPv4 and IPv6. Each switch comes with one SVI appearing in the default configuration "out-of-the-box." The default SVI is interface VLAN1.

Note: A Layer 2 switch does not need an IP address. The IP address assigned to the SVI is used to remotely access the switch. An IP address is not necessary for the switch to perform its operations.

To access the switch remotely, an IP address and a subnet mask must be configured on the SVI. To configure an SVI on a switch, use the interface vlan 1 global configuration command. Vlan 1 is not an actual physical interface but a virtual one. Next assign an IPv4 address using the ip address ip-address subnet-mask interface configuration command. Finally, enable the virtual interface using the no shutdown interface configuration command.

After these commands are configured, the switch has all the IPv4 elements ready for communication over the network.

Note: Similar to a Windows hosts, switches configured with an IPv4 address will typically also need to have a default gateway assigned. This can be done using the ip default-gateway ip-address global configuration command. The ip-address parameter would be the IPv4 address of the local router on the network, as shown in the example.

```console
Sw-Floor-1# configure terminal
Sw-Floor-1(config)# interface vlan 1
Sw-Floor-1(config-if)# ip address 192.168.1.20 255.255.255.0
Sw-Floor-1(config-if)# no shutdown            # <<< enable interface
Sw-Floor-1(config-if)# exit
Sw-Floor-1(config)# ip default-gateway 192.168.1.1
```

`show ip interface brief`




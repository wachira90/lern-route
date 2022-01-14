# Add and Delete Static Routes on macOS (persistently)

## Problem
I have several networks at home, including `192.168.1.0/24` and `192.168.2.0/24` A problem occurred when I connected to a VPN site because it gives a route with `192.168.2.0/23` So my traffic on `192.168.2.0/24` routed through the VPN tunnel instead of my internal home network.

Therefore, I need to add a static route on my MacBook Pro.

## Solution

Here is how to add or delete a static route on macOS.

As you see below, I received the `192.168.2.0/23` route from the VPN, and it routes through the tunnel interface, `utun3`. First, disconnect the VPN and add a static route as described below.

## To view the routing table:
You can use the following command `netstat -rn` and use `grep` to filter with a specific network on the Terminal.

````
macOS:/Users/analysisman% netstat -rn | grep 192.168.2.
192.168.2/23 1.1.1.1 UGSc utun3
````

### Method 1. Add a static route temporarily
````
To add a static route:

macOS:/Users/analysisman% sudo route -n add -net 192.168.2.0/24 192.168.1.1
add net 192.168.2.0: gateway 192.168.1.1


To verify the route you added:

macOS:/Users/analysisman% netstat -rn | grep 192.168.2.
192.168.2 192.168.1.1 UGSc en10
192.168.2/23 1.1.1.1 UGSc utun3

Now, 192.168.2.0/24 routes through my Ethernet interface, en10.


To delete a static route:

macOS:/Users/analysisman% sudo route -n delete 192.168.2.0/24
Password:
delete net 192.168.2.0

````

### Method 2. Add a static route persistently

The above route will be gone if you reboot your Mac. You need to add a static route permanently if you want to keep this route persistently.

#### To verify the route your interface:

````
macOS:/Users/analysisman% ifconfig -a
…snipped…

en10: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
options=6407<RXCSUM,TXCSUM,VLAN_MTU,CHANNEL_IO,PARTIAL_CSUM,ZEROINVERT_CSUM>
ether 00:24:9b:33:44:55
inet6 fe80::3f:e0d:4455:1ebe%en10 prefixlen 64 secured scopeid 0xb
inet 192.168.1.103 netmask 0xffffff00 broadcast 192.168.1.255
nd6 options=201<PERFORMNUD,DAD>
media: autoselect (1000baseT <full-duplex>)
````

#### To list devices (network adapters):
````
macOS:/Users/analysisman% networksetup -listallnetworkservices

An asterisk (*) denotes that a network service is disabled.
FT232R USB UART
USB 10/100/1000 LAN 2
USB 10/100/1000 LAN
USB 10/100/1000 LAN 3
USB 10/100/1000 LAN 4
USB 10/100/1000 LAN 5
Belkin USB-C LAN
Wi-Fi
iPhone USB 2
Bluetooth PAN
Thunderbolt Bridge
GlobalProtectDo
GlobalProtectDo 2
````
OR
#### To list devices with the interface number:

I prefer this command because it also shows the ethernet number (e.g. en10).

````
macOS:/Users/analysisman% networksetup -listnetworkserviceorder

An asterisk (*) denotes that a network service is disabled.
(1) FT232R USB UART
(Hardware Port: FT232R USB UART, Device: usbserial-AI06J8P5)

(2) USB 10/100/1000 LAN 2
(Hardware Port: USB 10/100/1000 LAN, Device: en8)

(3) USB 10/100/1000 LAN
(Hardware Port: USB 10/100/1000 LAN, Device: en10)
````

#### To add a static route permanently:
````
Usage:
networksetup -setadditionalroutes <networkservice> [ <dest> <mask> <gateway> ]*

macOS:/Users/analysisman% sudo networksetup -setadditionalroutes "USB 10/100/1000 LAN" 192.168.2.0 255.255.255.0 192.168.1.1
````

#### To verify the route you added:
````
macOS:/Users/analysisman% netstat -rn | grep 192.168.2.
192.168.2 192.168.1.1 UGSc en10
````

#### To delete this permanent route:

Use `sudo networksetup -setadditionalroutes interface-name` without the address, netmask, and gateway.
````
macOS:/Users/analysisman% sudo networksetup -setadditionalroutes "USB 10/100/1000 LAN"
````

### To see all commands:
````
networksetup -help
Or
networksetup -printcommands
````

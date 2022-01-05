# ubuntu command

## install 
````
apt install inetutils-traceroute -y
apt install traceroute -y
````

## traceroute

````
root@test-imac:~# traceroute google.co.th
traceroute to google.co.th (172.217.26.67), 64 hops max
  1   172.16.1.1  0.255ms  0.184ms  0.149ms 
  2   58.136.16.1  5.105ms  5.065ms  2.970ms 
  3   49.228.0.254  5.371ms  6.601ms  5.804ms 
  4   49.228.4.102  4.880ms  4.781ms  5.403ms 
  5   49.228.4.70  5.624ms  5.127ms  5.557ms 
  6   49.231.44.129  35.138ms  16.182ms  16.067ms 
  7   103.3.64.242  31.449ms  31.390ms  32.168ms 
  8   72.14.202.218  29.028ms  28.784ms  28.781ms 
  9   72.14.234.96  33.875ms  35.725ms  34.203ms 
 10   142.251.231.134  31.913ms  31.985ms  31.623ms 
 11   172.217.26.67  26.694ms  26.495ms  26.554ms 
root@test-imac:~#
````

## route command
````
docker@test-imac:~/web_site$ ip route
default via 172.16.1.1 dev enp3s0f0 proto dhcp src 172.16.1.5 metric 100 
172.16.1.0/24 dev enp3s0f0 proto kernel scope link src 172.16.1.5 
172.16.1.1 dev enp3s0f0 proto dhcp scope link src 172.16.1.5 metric 100 
172.16.16.0/24 dev br-43760f592dc9 proto kernel scope link src 172.16.16.1 
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown 
172.20.0.0/16 dev br-088a5d2de318 proto kernel scope link src 172.20.0.1 
172.21.0.0/16 dev br-2a2a968cad53 proto kernel scope link src 172.21.0.1 
172.23.0.0/16 dev br-2495835085ed proto kernel scope link src 172.23.0.1 
172.28.0.0/16 dev br-7640b13c17a8 proto kernel scope link src 172.28.0.1 
192.168.192.0/20 dev br-4d389140e717 proto kernel scope link src 192.168.192.1 
192.168.224.0/20 dev br-3ae7b552cee6 proto kernel scope link src 192.168.224.1 
docker@test-imac:~/web_site$
````

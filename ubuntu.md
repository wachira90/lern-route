# ubuntu command

## install 
````
apt install inetutils-traceroute
apt install traceroute
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

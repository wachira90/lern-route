# lern-route
lern-route

## show route windows 

````
route print
````
OR
````
netstat -r
````

## show route mac 

````
netstat -r
````

## check route windows
````
tracert 192.168.4.12
````

## check route mac
````
traceroute 192.168.4.12
````

## add route mac
````
sudo route -n add -net 192.168.4.0/24 172.16.1.1
````

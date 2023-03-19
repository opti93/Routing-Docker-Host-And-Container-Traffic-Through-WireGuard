#Routing Docker Host And Container Traffic Through WireGuard container

#
```sh
docker-compose up -d
```
#### Route to specific ip
```sh
sudo route add -net 165.156.72.197 netmask 255.255.255.255 gw 172.20.0.50
```

#### Setting up as default route
To put all traffic through wireguard container you need delete default gataeway,
add route to wireguard server throught default gataway of your network and put all traffic through wireguad container ip.

```sh
sudo ip route del default
sudo ip route add 89.45.90.197 via 192.168.1.1
sudo ip route add default via 172.20.0.50
```

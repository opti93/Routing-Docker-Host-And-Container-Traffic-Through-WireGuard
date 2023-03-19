### Put your wireguard config in ./config/wg0.conf

```sh
[Interface]
PrivateKey = "your private key"
ListenPort = 51820
Address = 10.13.13.2/32
DNS = 8.8.8.8
PostUp = iptables -t nat -A POSTROUTING -o wg+ -j MASQUERADE
PreDown = iptables -t nat -D POSTROUTING -o wg+ -j MASQUERADE

[Peer]
PublicKey = "your public key"
PresharedKey = "your preshared key"
AllowedIPs = 0.0.0.0/0
Endpoint = "wireguard-server-ip:51820"
```

#
```sh
docker-compose up -d
```
#### Route to specific ip
```sh
sudo route add -net 165.156.72.197 netmask 255.255.255.255 gw 172.20.0.50
```
165.156.72.197 - change to desire ip that you want to reach

#### Setting up as default route
To put all traffic through wireguard container you need delete default gateway,
add route to wireguard server throught default gataway of your network and put all traffic through wireguad container ip.

```sh
sudo ip route del default
sudo ip route add 89.45.90.197 via 192.168.1.1
sudo ip route add default via 172.20.0.50
```

89.45.90.197 - change to your wireguard server ip<br/>
192.168.1.1  - change to your default gateway ip

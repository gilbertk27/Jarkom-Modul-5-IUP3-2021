# Jarkom-Modul-5-IUP3-2021

Setelah kalian mempelajari semua modul yang telah diberikan, Luffy ingin meminta bantuan untuk terakhir kalinya kepada kalian. Dan kalian dengan senang hati mau membantu Luffy.

## A. Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Luffy dibawah ini:

#### Keterangan : 

Doriki adalah DNS Server

Jipangu adalah DHCP Server

Maingate dan Jorge adalah Web Server

Jumlah Host pada Blueno adalah 100 host

Jumlah Host pada Cipher adalah 700 host

Jumlah Host pada Elena adalah 300 host

Jumlah Host pada Fukurou adalah 200 host

--Foto Subnetting--

## B. Karena kalian telah belajar subnetting dan routing, Luffy ingin meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM.


| Subnet | Node | IP | Subnet Mask | Length |
| --- | --- | --- | --- | --- |
| A | WATER7 | 10.39.7.1 | 255.255.255.128 | /25 |
| A | Blueno | 10.39.7.2 | 255.255.255.128 |  |
| B | WATER7 | 10.39.7.129 | 255.255.255.248 | /29 |
| B | Doriki | 10.39.7.130 | 255.255.255.248 |  |
| B | Jipangu | 10.39.7.131 | 255.255.255.248 |  |
| C | WATER7 | 10.39.0.1 | 255.255.252.0 | /22 |
| C | Cipher | 10.39.0.2 | 255.255.252.0 |  |
| D | FOOSHA | 10.39.7.145 | 255.255.255.252 | /30 |
| D | WATER7 | 10.39.7.146 | 255.255.255.252 |  |
| E | FOOSHA | 10.39.7.149 | 255.255.255.252 | /30 |
| E | GUANHAO | 10.39.7.150 | 255.255.255.252 |  |
| F | GUANHAO | 10.39.6.1 | 255.255.255.0 | /24 |
| F | Elena | 10.39.6.2 | 255.255.255.0 |  |
| G | GUANHAO | 10.39.7.137 | 255.255.255.248 | /29 |
| G | Jorge | 10.39.7.138 | 255.255.255.248 |  |
| G | Maingaete | 10.39.7.139 | 255.255.255.248 |  |
| H | GUANHAO | 10.39.4.1 | 255.255.254.0 | /23 |
| H | Fukurou | 10.39.4.2 | 255.255.254.0 |  |

--Foto Pohon--

### CONFIG NODE

#### FOOSHA
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
hwaddress ether 5e:0d:2e:c6:9b:9a

auto eth1
iface eth1 inet static
	address 10.39.7.145
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.39.7.149
	netmask 255.255.255.252
```

#### WATER7
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
	address 10.39.7.146
	netmask 255.255.255.252
  	gateway 10.39.7.145
  
auto eth1
iface eth1 inet static
	address 10.39.7.1
	netmask 255.255.255.128
  
auto eth2
iface eth2 inet static
  address 10.39.7.129
  netmask 255.255.255.248


auto eth3
iface eth3 inet static
  address 10.39.0.1
  netmask 255.255.252.0
```

#### GUANHAO
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
	address 10.39.7.150
	netmask 255.255.255.252
  	gateway 10.39.7.149
  
auto eth1
iface eth1 inet static
	address 10.39.6.1
	netmask 255.255.255.0
  
auto eth2
iface eth2 inet static
  address 10.39.7.137
  netmask 255.255.255.248


auto eth3
iface eth3 inet static
  address 10.39.4.1
  netmask 255.255.254.0
```

#### Blueno
```
auto eth0
iface eth0 inet static
#auto eth0
#iface eth0 inet dhcp
	address 10.39.7.2
	netmask 255.255.255.128
	gateway 10.39.7.1
```

#### Doriki
```
auto eth0
iface eth0 inet static
	address 10.39.7.130
	netmask 255.255.255.248
	gateway 10.39.7.129	
```

#### Jipangu
```
auto eth0
iface eth0 inet static
	address 10.39.7.131
	netmask 255.255.255.248
	gateway 10.39.7.129
```

#### Cipher
```
auto eth0
iface eth0 inet static
#auto eth0
#iface eth0 inet dhcp
	address 10.39.0.2
	netmask 255.255.252.0
	gateway 10.39.0.1
```

#### Fukurou
```
auto eth0
iface eth0 inet static
#auto eth0
#iface eth0 inet dhcp
	address 10.39.4.2
	netmask 255.255.254.0
	gateway 10.39.4.1
```

#### Maingate
```
auto eth0
iface eth0 inet static
	address 10.39.7.139
	netmask 255.255.255.248
	gateway 10.39.7.137
```

#### Jorge
```
auto eth0
iface eth0 inet static
	address 10.39.7.138
	netmask 255.255.255.248
	gateway 10.39.7.137
```

#### Elena
```
auto eth0
iface eth0 inet static
#auto eth0
#iface eth0 inet dhcp
	address 10.39.6.2
	netmask 255.255.255.0
	gateway 10.39.6.2
```

## C. Setelah melakukan subnetting, Kalian juga diharuskan melakukan Routing agar setiap perangkat pada jaringan tersebut dapat terhubung.

### Routing

#### FOOSHA
```
# !/bin/sh

route add -net 10.39.7.0 netmask 255.255.255.128 gw 10.39.7.146
route add -net 10.39.7.128 netmask 255.255.255.248 gw 10.39.7.146
route add -net 10.39.0.0 netmask 255.255.252.0 gw 10.39.7.146

route add -net 10.39.6.0 netmask 255.255.255.0 gw 10.39.7.150
route add -net 10.39.7.136 netmask 255.255.255.248 gw 10.39.7.150
route add -net 10.39.4.0 netmask 255.255.254.0 gw 10.39.7.150
```

#### nano ./.bashrc
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.39.0.0/16
/root/config.sh
echo "nameserver 10.39.122.1" > /etc/resolv.conf
```

-- Foto Routing--

## D. Tugas berikutnya adalah memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

### Doriki (DNS Server)

##### nano config.sh
```
# !/bin/sh

apt-get update
apt-get install bind9 -y
```

### Jipangu (DHCP Server)

##### nano config.sh
```
# !/bin/sh

apt-get update
apt-get install isc-dhcp-server -y
```

##### nano isc-dhcp-server
```
INTERFACES="eth0"
```

#### nano dhcpd.conf
```
# Blueno
subnet 10.39.7.0 netmask 255.255.255.128 {
    range 10.39.7.2 10.39.7.126;
    option routers 10.39.7.1;
    option broadcast-address 10.39.7.127;
    option domain-name-servers 10.39.7.130;
    default-lease-time 360;
    max-lease-time 7200;
}

# Cipher
subnet 10.39.0.0 netmask 255.255.252.0	 {
    range 10.39.0.2 10.39.3.254;
    option routers 10.39.0.1;
    option broadcast-address 10.39.3.255;
    option domain-name-servers 10.39.7.130;
    default-lease-time 720;
    max-lease-time 7200;
}

# Fukurou
subnet 10.39.4.0 netmask 255.255.254.0 {
    range 10.39.4.2 10.39.5.254;
    option routers 10.39.4.1;
    option broadcast-address 10.39.5.255;
    option domain-name-servers 10.39.7.130;
    default-lease-time 720;
    max-lease-time 7200;
}

# Elena
subnet 10.39.6.0 netmask 255.255.255.0 {
    range 10.39.6.2 10.39.6.254;
    option routers 10.39.6.1;
    option broadcast-address 10.39.6.255;
    option domain-name-servers 10.39.7.130;
    default-lease-time 720;
    max-lease-time 7200;
}

# Routing dari Jipangu ke router Water7
subnet 10.39.7.128 netmask 255.255.255.248 {
        option routers 10.39.7.129;
}

# Routing dari Jipangu ke router Guanhao
subnet 10.39.7.136 netmask 255.255.255.248 {
        option routers 10.39.7.137;
}

# Routing dari Jipangu ke router Foosha
subnet 10.39.7.144 netmask 255.255.255.252 {
        option routers 10.39.7.145;
}

# Routing dari Foosha ke Guanhao
subnet 10.39.7.148 netmask 255.255.255.252 {
        option routers 10.39.7.149;
}

# Water7
#subnet 10.39.7.144 netmask 255.255.255.252 {
#        option routers 10.39.7.145;
#}

# Guanhao
#subnet 10.39.7.148 netmask 255.255.255.252 {
#        option routers 10.39.7.149;
#}

host FOOSHA {
    hardware ethernet 5e:0d:2e:c6:9b:9a;
    fixed-address 192.168.122.98;
}
```

### Water7 (DHCP Relay)

##### nano config.sh
```
# !/bin/sh

apt-get update
apt-get install isc-dhcp-relay -y

service isc-dhcp-relay start
```

##### nano /etc/default/isc-dhcp-relay
```
# What servers should the DHCP relay forward requests to?
SERVERS="10.39.7.131"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth1 eth2 eth3"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```

### Guanhao (DHCP Relay)

##### nano config.sh
```
# !/bin/sh

apt-get update
apt-get install isc-dhcp-relay -y

service isc-dhcp-relay start
```

##### nano /etc/default/isc-dhcp-relay
```
# What servers should the DHCP relay forward requests to?
SERVERS="10.39.7.131"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth1 eth2 eth3"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```

### Maingate (Web Server)

##### nano config.sh
```
# !/bin/sh

apt-get update
apt-get install isc-dhcp-relay -y

service isc-dhcp-relay start
```

### Jorge (Web Server)

##### nano config.sh
```
# !/bin/sh

apt-get update
```

### Blueno (Client)

#### All

Config ditambah:
```
auto eth0
iface eth0 inet dhcp
```

##### nano config.sh
```
# !/bin/sh

```

### Cipher
```
# !/bin/sh

```

### Fukurou
```
# !/bin/sh

```

### Elena
```
# !/bin/sh

```
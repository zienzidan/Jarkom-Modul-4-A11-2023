# Jarkom-Modul-3-A11-2023

**Praktikum Jaringan Komputer Modul 3 Tahun 2023**

## Penulis

| Nama                | NRP        | Github                         |
| ------------------- | ---------- | ------------------------------ |
| Muhammad Zien Zidan | 5025211122 | https://github.com/zienzidan   |
| Glenaya             | 5025211202 | https://github.com/nyawnayaw05 |

## Topologi

![first](image/1.topologi.png)

## Soal

Dalam soal praktikum kali ini, kita disajikan dengan sebuah topologi yang memerlukan penyelesaian melalui Cisco Packet Tracer dan GNS3. Tugas yang diberikan menuntut penerapan metode perhitungan CLASSLESS yang berbeda satu sama lain.
Selain itu, kita juga harus membagi IP dan routing se-efisien mungkin.

## Jawaban

Disini kita sepakat untuk menggunakan metode VLSM pada GNS3 dan metode CIDR pada Cisco Packet Tracer.

### Langkah Ke 1

> Kita harus menentukan rute dari topologi yang sudah diberikan

Berikut rute yang kami temukan
![first](image/2.rute.jpg)

agar lebih jelas, kami juga mengisi sheet yang telah ditentukan.
![first](image/3.rute.png)

### Langkah Ke 2

> Tentukan Pembagian IP pada VLSM

Berikut merupakan sheet pembagian IP pada VLSM
![Alt text](image/Pembagian%20IP%20VLSM.png)

## CIDR
### Langkah Ke 1

> Lakukan Penggabungan rute hingga menjadi satu kesatuan agar dapat dibuat pembagian IP CIDR

Lakukan penggabungan Subnet B

![first](image/4.penggabungan.jpg)

![first](image/12.penggabunganB.png)

Lakukan penggabungan Subnet c

![first](image/5.penggabungan.jpg)

![first](image/13.penggabunganC.png)

Lakukan penggabungan Subnet D

![first](image/6.penggabungan.jpg)

![first](image/14.penggabunganD.png)

Lakukan penggabungan Subnet E

![first](image/7.penggabungan.jpg)

![first](image/15.penggabunganE.png)

Lakukan penggabungan Subnet F

![first](image/8.penggabungan.jpg)

![first](image/16.penggabunganF.png)

Lakukan penggabungan Subnet G

![first](image/9.penggabungan.jpg)

![first](image/17.penggabunganG.png)

Lakukan penggabungan Subnet H

![first](image/10.penggabungan.jpg)

![first](image/18.penggabunganH.png)

Lakukan penggabungan Subnet I

![first](image/11.penggabungan.jpg)

![first](image/19.penggabunganI.png)

### Langkah Ke 2

> Setelah mendapatkan penggabungan CIDR lakukan pembagian IP untuk CIDR

Lakukan pembuatan tree untuk pembagian CIDR

![first](image/20.CIDR-A11_Modul%204.jpg)

Lalu tentukan Network ID dan Broadcast untuk CIDR

![first](image/21.pembagianCIDR.png)

Selanjutnya tentukan alamat IP dengan cara diantara NetworkID hingga Brodcast disetiap subnet, sehingga nantinya akan digunakan untuk subnetting pada setiap node nya (router, client,server dan lain lain).

![first](image/22.subnetting.png)

dan lakukan testing dengan cara mengirim pesan pada node yang sejalan
seperti contoh ApppetitRegion dan LaubHills mengirim pesan kepada router fern

![first](image/23.subnetting.png)

Terakhir, lakukan routing di setiap node nya agar saling terhubung dan menjadikan Aura sebagai router tertinggi.

Seperti yang akan saya contohkan ialah melakukan routing dari Fern dan himmel ke Flamme

![first](<image/24%20(1).png>)

Lakukan config static didalam setiap node router

> Fern

isi config static seperti dibawah ini (agar memberikan permission ke router yang dituju)

```
Network     : 0.0.0.0
Mask        : 0.0.0.0
Next Hop    : 192.174.152.1 (Isi sesuai IP FastEthernet yang mengakses ke Flamme)
```

![first](<image/25%20(1).png>)

> Himmel

isi config static seperti dibawah ini (agar memberikan permission ke router yang dituju)

```
Network     : 0.0.0.0
Mask        : 0.0.0.0
Next Hop    : 192.174.128.9 (Isi sesuai IP FastEthernet yang mengakses ke Flamme)
```

![first](<image/25%20(2).png>)

> Flamme

isi config static router yang mengakses router lain
seperti contoh dibawah ini flamme mengakses subnet A5 milik Fern

```
Network     : 192.174.144.0 (Isi sesuai subnet yang ingin diakses)
Mask        : 255.255.248.0 (isi sesuai netmask dari subnet tersebut)
Next Hop    : 192.174.152.2 (Isi sesuai IP FastEthernet yang mengakses ke Fern)
```

Lakukan hal sebaliknya mengakses Subnet A8 milik Himmel

```
Network     : 192.174.128.0 (Isi sesuai subnet yang ingin diakses)
Mask        : 255.255.255.248 (isi sesuai netmask dari subnet tersebut)
Next Hop    : 192.174.128.10 (Isi sesuai IP FastEthernet yang mengakses ke Fern)
```

Lakukan juga permission ke dalam router Frieren

```
Network     : 0.0.0.0
Mask        : 0.0.0.0
Next Hop    : 192.174.136.1 (Isi sesuai IP FastEthernet yang mengakses ke Frieren)
```

![first](<image/25%20(3).png>)

Lakukan hal yang sama di dalam router Frieren yaitu dengan mengakses subnet yang dibutuhkan dan memberikan permission ke router utama yaitu Aura agar bisa saling terhubung

![first](image/26.Frieren.png)

Lakukan hal yang sama ke dalam router Eisen dan Denken bilamana ada sub router atau router yang lebih kecil lakukan pengaksesan dan permission kepada router yang lebih besar.

Didalam router Aura lakukan pengaksesan kepada seluruh subnet kecuali subnet yang sudah terhubung seperti A3, A9, A20

![first](image/27.Aura.png)

Aura hanya boleh mengakses subnet dan tidak memberikan permission karena aura disini bertindak sebagai router utama yang harus bertindak secara adil.

![first](image/28.Aura.png)

> Testing

Lakukan pengiriman pesan atau ping ke alamat IP yang dituju

![first](image/29.tes.png)

## VLSM
### Konfigurasi Network
- Aura
 ```shell
 auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.174.0.1
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.174.0.37
	netmask 255.255.255.252

auto eth3
iface eth3 inet static
	address 192.174.0.17
	netmask 255.255.255.252
 ```

- Denken
```shell
auto eth0
iface eth0 inet static
	address 192.174.0.38
	netmask 255.255.255.252
	gateway 192.174.0.37

auto eth1
iface eth1 inet static
	address 192.174.2.1
	netmask 255.255.255.0
```

- Frieren
```shell
auto eth0
iface eth0 inet static
	address 192.174.0.5
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 192.174.0.65
	netmask 255.255.255.224

auto eth2
iface eth2 inet static
	address 192.174.0.2
	netmask 255.255.255.252
	gateway 192.174.0.1

```

- Flamme
```shell
auto eth0
iface eth0 inet static
	address 192.174.0.9
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 192.174.8.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.174.0.13
	netmask 255.255.255.252

auto eth3
iface eth3 inet static
	address 192.174.0.6
	netmask 255.255.255.252
	gateway 192.174.0.5
```
- Fern
```shell
auto eth0
iface eth0 inet static
	address 192.174.24.1
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 192.174.0.10
	netmask 255.255.255.0
	gateway 192.174.0.9
```
- Himmel
```shell
auto eth0
iface eth0 inet static
	address 192.174.0.14
	netmask 255.255.255.252
	gateway 192.174.0.13

auto eth1
iface eth1 inet static
	address 192.174.0.41
	netmask 255.255.255.248
```
- Eisen
```shell
auto eth0
iface eth0 inet static
	address 192.174.0.18
	netmask 255.255.255.252
	gateway 192.174.0.17

auto eth1
iface eth1 inet static
	address 192.174.0.49
	netmask 255.255.255.248

auto eth2
iface eth2 inet static
	address 192.174.0.25
	netmask 255.255.255.252

auto eth3
iface eth3 inet static
	address 192.174.0.21
	netmask 255.255.255.252

auto eth4
iface eth4 inet static
	address 192.174.0.29
	netmask 255.255.255.252
```
- Lugner
```shell
auto eth0
iface eth0 inet static
	address 192.174.0.26
	netmask 255.255.255.252
	gateway 192.174.0.25

auto eth1
iface eth1 inet static
	address 192.174.12.1
	netmask 255.255.255.0
auto eth2
iface eth2 inet static
	address 192.174.1.1
	netmask 255.255.255.0
```
- Linie
```shell
auto eth0
iface eth0 inet static
	address 192.174.4.1
	netmask 255.255.254.0

auto eth1
iface eth1 inet static
	address 192.174.0.33
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.174.0.30
	netmask 255.255.255.252
	gateway 192.174.0.29
```
- Lawine
```shell
auto eth0
iface eth0 inet static
	address 192.174.0.34
	netmask 255.255.255.252
	gateway 192.174.0.33

auto eth1
iface eth1 inet static
	address 192.174.0.129
	netmask 255.255.255.192
```
- Heiter
```shell
auto eth0
iface eth0 inet static
	address 192.174.0.130
	netmask 255.255.255.192
	gateway 192.174.0.129

auto eth1
iface eth1 inet static
	address 192.174.16.1
	netmask 255.255.255.0
```
- AppetitRegion
```shell
auto eth0
iface eth0 inet static
	address 192.174.24.2
	netmask 255.255.248.0
	gateway  192.174.24.1
```

- LaubHills
```shell
auto eth0
iface eth0 inet static
	address 192.174.24.3
	netmask 255.255.248.0
	gateway 192.174.24.1
```

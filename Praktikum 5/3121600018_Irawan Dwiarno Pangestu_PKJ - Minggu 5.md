# VLAN DAN ROUTER ON STICK

## 1. Topologi Jaringan

<img src="assets/1.png">

## 2. Konfigurasi
- Konfigurasi IP PC0
<img src="assets/2.png">

- Konfigurasi IP PC1
<img src="assets/3.png">

- Konfigurasi Router On Stick pada Router
<img src="assets/4.png">
-> Sub-interface Gig0/0/0.10 untuk default gateway VLAN 10 </br>
-> Sub interface Gig0/0/0.30 untuk default gateway VLAN 30

- Konfigurasi Vlan 10 dan Vlan 30 pada Switch
<img src="assets/5.png">
VLAN 10 dan VLAN 30 sudah ada, namun tidak memiliki PORT

- Mode access untuk interface 0/1 ke VLAN 10 dan 0/2 ke VLAN 30 pada Switch yang terhubung pada PC,
- Mode trunk untuk interface 0/3 yang terhubung dengan Router 
<img src="assets/6.png">

- Mengecek PORT VLAN 10 dan VLAN 30
<img src="assets/7.png">
-> VLAN 10 memiliki PORT 0/1 </br>
-> VLAN 30 memiliki PORT 0/2

## 3. Ping dari PC0 ke PC1
<img src="assets/8.png">




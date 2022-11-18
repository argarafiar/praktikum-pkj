## KELOMPOK 4
|Arga Rafi I.M |(3121600010)|
|Muhammad Faishal Nabhan |(3121600021)|
|Muh Khozinatul Asror |(3121600026)|

## A. Topologi
[![Screenshot-2022-11-17-143634.jpg](https://i.postimg.cc/pTYRGm47/Screenshot-2022-11-17-143634.jpg)](https://postimg.cc/S2sBjxy7)

Topologi di atas terdiri dari 10 router. R1 sebagai router utama yang menghubungkan ke nomor AS lainnya. area R2 menggunakan protokol routing RIP, area R3 menggunakan OSPF, area R4 menggunakan routing statis, sedangkan area R2, R3 dan R4 menggunakan protokol routing BGP untuk terhubung ke router pusat yaitu R1 yang terhubung.

| Devices |   IP Address    | CIDR |     Network     | Interface |
| :-----: | :-------------: | :--: | :-------------: | :-------: |
|   R1    |   14.14.14.1    |  24  |   14.14.14.0    |  ether2   |
|         |   13.13.13.1    |  24  |   13.13.13.0    |  ether3   |
|         |   12.12.12.1    |  24  |   12.12.12.0    |  ether4   |
|   R2    |   12.12.12.2    |  24  |   12.12.12.0    |  ether1   |
|         |   27.27.27.2    |  24  |   27.27.27.0    |  ether2   |
|         |   28.28.28.2    |  24  |   28.28.28.0    |  ether3   |
|   R3    |   13.13.13.3    |  24  |   13.13.13.0    |  ether1   |
|         |   36.36.36.3    |  24  |   36.36.36.0    |  ether2   |
|         |   35.35.35.3    |  24  |   35.35.35.0    |  ether3   |
|   R4    |   14.14.14.4    |  24  |   14.14.14.0    |  ether1   |
|         |   41.41.41.4    |  24  |   41.41.41.0    |  ether2   |
|         |   49.49.49.4    |  24  |   49.49.49.0    |  ether3   |
|   R5    |   35.35.35.5    |  24  |   35.35.35.0    |  ether1   |
|         |   50.50.50.50   |  -   |   50.50.50.50   |    lo0    |
|   R6    |   36.36.36.6    |  24  |   36.36.36.0    |  ether1   |
|         |   60.60.60.60   |  -   |   60.60.60.60   |    lo0    |
|   R7    |   27.27.27.7    |  24  |   27.27.27.0    |  ether1   |
|         |   70.70.70.70   |  -   |   70.70.70.70   |    lo0    |
|   R8    |   28.28.28.8    |  24  |   28.28.28.0    |  ether1   |
|         |   80.80.80.80   |  -   |   80.80.80.80   |    lo0    |
|   R9    |   49.49.49.9    |  24  |   49.49.49.0    |  ether1   |
|         |   90.90.90.90   |  -   |   90.90.90.90   |    lo0    |
|   R10   |   41.41.41.10   |  24  |   41.41.41.0    |  ether1   |
|         | 100.100.100.100 |  -   | 100.100.100.100 |    lo0    |

## B. Ruang Lingkup Kerja

Dalam pratikum kali ini kelompok kami bertugas untuk mengatur router R4 yng menggunakan routing static sesuai area yang telah ditentukan. Kami melakukan konfigurasi routing (routing Static) tersebut dengan perintah sebagai berikut:

    /ip route
    add distance=1 dst-address=90.90.90.90/32 gateway=49.49.49.9
    add distance=1 dst-address=100.100.100.100/32 gateway=41.41.41.10

## C. Table Routing

[![Screenshot-505.png](https://i.postimg.cc/cJ1qmdf1/Screenshot-505.png)](https://postimg.cc/YvPy2KXT)

Terlihat dengan perintah ip route print untuk melihat isi tabel routing, bahwa router R4 sudah terhubung dengan router R9 dan R10 yang menggunakan routing protocol static. Selain itu, router R4 juga terhubung dengan router R1 yang menggunakan routing protocol Static dan terhubung dengan router R2 yang menggunakan routing protocol BGP.

## D. Test Koneksi

[![Screenshot-506.png](https://i.postimg.cc/B6GmggrT/Screenshot-506.png)](https://postimg.cc/Y4bN21q0)

[![Screenshot-507.png](https://i.postimg.cc/V61FMNt4/Screenshot-507.png)](https://postimg.cc/3ySpQYnD)

[![Screenshot-508.png](https://i.postimg.cc/R0x150g9/Screenshot-508.png)](https://postimg.cc/gx4L3G9B)

[![Screenshot-509.png](https://i.postimg.cc/j5gJ5q4D/Screenshot-509.png)](https://postimg.cc/LYPsQp7S)

[![Screenshot-510.png](https://i.postimg.cc/KvggG2kY/Screenshot-510.png)](https://postimg.cc/fJDbC1v4)

[![Screenshot-511.png](https://i.postimg.cc/284hdYzK/Screenshot-511.png)](https://postimg.cc/crLvZVtR)

Gambar-gambar di atas merupakan test koneksi dengan perintah ping ke IP Address yang telah ditentukan.

- Berhasil melakukan ping ke IP Address pada router R10 (41.41.41.10), R9 (49.49.49.9), R2 (12.12.12.2), R3 (13.13.13.3) yang tentu saja berhasil karena sudah memiliki routing tabel dengan tujuan ke network berikut.
- Gagal melakukan ping ke IP Address pada router R8 (28.28.28.0) dan R7 (27.27.27.7) dan R5 (35.35.35.5) R6 (36.36.36.6) karena tidak memiliki routing tabel dengan tujuan ke network di atas. Sepertinya masalah karena tidak menerima routing tabel dari R2 dan R3 secara penuh, hanya menerima routing tabel sebatas dengan router R1 saja.
# Dynamic Routing With Protcol RIP
## Dynamic Routing

Perutean dinamis adalah metode perutean yang memungkinkan router menemukan rute ke jaringan tanpa konfigurasi manual. Perutean dinamis menggunakan protokol perutean untuk menentukan rute ke jaringan. Protokol routing yang digunakan dalam percobaan ini adalah RIP (Routing Information Protocol). Beginilah cara kerja perutean dinamis:
1. Router mengirimkan routing table ke semua router yang terhubung pada jaringan.
2. Router yang menerima routing table akan melakukan update routing table sesuai dengan routing table yang diterima.
3. Setelah update routing table, router akan mengirimkan routing table yang sudah diupdate ke semua router yang terhubung pada jaringan.
4. Langkah 2 dan 3 akan terus berulang sampai semua router pada jaringan memiliki routing table yang sama.

## Routing Information Protocol (RIP)

RIP adalah protokol routing yang digunakan untuk melakukan routing di jaringan IP. RIP menggunakan metode distance vector untuk menentukan rute ke jaringan.

Metode distance vector ini merupakan metode routing yang menggunakan vektor jarak untuk menentukan rute ke jaringan. Vektor jarak ini adalah jarak dari router ke jaringan. Vektor jarak ini disebut hop count. Hitungan hop adalah jumlah router yang dilalui untuk mencapai jaringan.

RIP juga menggunakan siaran untuk memperbarui tabel perutean dan membagi cakrawala untuk menghindari loop perutean. Cara kerja RIP adalah menghitung jarak dari suatu router ke suatu jaringan dengan menghitung jumlah router yang dilaluinya untuk mencapai jaringan tersebut. Semakin sedikit router yang dilalui, semakin pendek jaraknya. Jarak pendek meneruskan paket secara istimewa melalui jarak jauh.

## Praktek Dynamic Routing (RIP)
### Topologi

![](https://raw.githubusercontent.com/argarafiar/praktikum-pkj/main/minggu9/asset/WhatsApp%20Image%202022-10-20%20at%2013.46.39.jpeg)

Topologi di atas masih sama dengan minggu lalu, yang membedakan adalah penggunaan dynamic routing dengan RIP. Perutean statis digunakan minggu lalu.

### Konfigurasi IP Router

| Device | Interface | IP |
| ------ | ------ | ------ |
| Route 0 | Fa0/0 | 192.168.2.2 |
|  | Fa0/1 | 192.168.1.2 |
|Router 1 | Fa0/0 | 192.168.1.1 |
|  | Fa0/1 | 192.168.3.2 |
|  | Fa0/2 | 192.168.4.1 |
| Router 2 | Fa0/0 | 192.168.2.1 |
|  | Fa0/1 | 192.168.3.1 |
|  | Fa0/2 | 192.168.5.1 |

### Konfigurasi IP PC

| Device | Interface | IP |
| ------ | ------ | ------ |
| PC0 | Fa0/0 | 192.168.4.2 |
| PC1 | Fa0/0 | 192.168.5.2 |

### Konfigurasi Routing (RIP)

| Device | Network |
| ------ | ------ |
| Route 0 | 192.168.1.0 |
|  | 192.168.2.0 |
|Router 1 | 192.168.1.0 |
|  | 192.168.3.0 |
|  | 192.168.5.0 |
| Router 2 | 192.168.2.0 |
|  | 192.168.3.0 |
|  | 192.168.4.0 |

Contoh perintah yang digunakan pada router 0 untuk mengaktifkan RIP adalah:
```sh
Router(config)#router rip
Router(config-router)#network 192.168.1.0
Router(config-router)#network 192.168.2.0
```

### Testing

![](https://raw.githubusercontent.com/argarafiar/praktikum-pkj/main/minggu9/asset/WhatsApp%20Image%202022-10-20%20at%2013.44.20.jpeg)
![]()

Kita dapat melihat bahwa jalur yang diambil oleh paket yang dikirim dari PC0 ke PC1 adalah:
1. PC0 mengirimkan paket ke router 1.
2. Router 2 menerima paket dan mengirimkan paket ke router 1.
3. Router 2 menerima paket dan mengirimkan paket ke PC1.
4. PC1 menerima paket.

Karena tracert di atas adalah upaya pertama, Router 2 tidak memiliki tabel routing. Setelah Router 2 menerima tabel perutean Router 1, ia memperbarui tabel peruteannya. Ada penundaan waktu karena tabel perutean belum diperbarui.
# Traceroute And Time To Live
## Traceroute
Traceroute adalah perintah yang menampilkan rute yang diambil paket untuk mencapai tujuannya. Ini dilakukan dengan mengirimkan pesan Internet Control Message Protocol Echo Request ke tujuan dengan nilai time-to-live yang meningkat. Dalam sistem operasi Windows, traceroute ini disebut tracert.

Pembacaan traceroute biasanya mengembalikan tiga kolom waktu hop yang terpisah, karena setiap traceroute mengirimkan tiga informasi terpisah ke setiap komputer. Di bagian paling atas daftar, traceroute akan membatasi jumlah lompatan baris yang akan ditampilkan. Biasanya, jumlah maksimum adalah sekitar 30 hop.

Pesan "Permintaan habis waktu" muncul ketika traceroute tidak dapat menjangkau komputer. Setiap kolom hop akan menampilkan tanda bintang, bukan milidetik.

## Time To Live
Time to Live atau hop adalah mekanisme untuk membatasi usia atau masa pakai data di komputer atau jaringan. Nilai TTL menentukan bahwa paket harus diteruskan ke router hop berikutnya atau dijatuhkan. Nilai TTL default adalah 64, maksimum 255 (8 bit), setiap paket melewati router (layer 3), nilainya akan dikurangi 1 sebelum keputusan penerusan, jika TTL, router tidak akan melewati lalu lintas ke rute berikutnya ia menerima 1

## Topologi
![](https://raw.githubusercontent.com/argarafiar/praktikum-pkj/main/minggu8/asset/WhatsApp%20Image%202022-10-16%20at%2009.19.46.jpeg)
Topologi diatas terdiri dari 3 router, 2 PC, dan 2 switch. Jenis router yang digunakan adalah Router-PT yang memiliki port-port yang dimodifikasi sesuai kebutuhan.

## Konfigurasi IP PC
| Device | Interface | IP |
| ------ | ------ | ------ |
| PC0 | Fa0/0 | 192.168.4.2 |
| PC1 | Fa0/0 | 192.168.5.2 |

## Konfigurasi IP Router
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

## Konfigurasi Static Routing pada Router
| Device | Destination Network | Netmask | Via | Metric |
| ------ | ------ | ------ | ------ | ------ |
| Router 0	 | 192.168.4.0	 | 255.255.255.0 | 192.168.2.1 | 10 (Default) |
|  | 192.168.5.0 | 255.255.255.0 | 192.168.1.1 | 10 (Default) |
| Router 1 | 192.168.4.0 | 255.255.255.0 | 192.168.3.1 | 10 (Default) |
|  | 192.168.2.0 | 255.255.255.0 | 192.168.1.2 | 10 (Default) |
| Router 2 | 192.168.5.0 | 255.255.255.0 | 192.168.3.1 | 10 (Default) |
|  | 192.168.1.0 | 255.255.255.0 | 192.168.2.2 | 10 (Default) |
Pada konfigurasi static routing di atas dapat dilakukan dengan memasukkan perintah pada CLI. Struktur perintah yang menyediakan konfigurasi di atas adalah sebagai berikut, "ip route [jaringan tujuan] [netmask] [via] [metrik]".

## Percobaan Traceroute / Tracert
Perintah untuk mengeksekusi traceroute atau tracert adalah sebagai berikut.
![](https://raw.githubusercontent.com/argarafiar/praktikum-pkj/main/minggu8/asset/WhatsApp%20Image%202022-10-16%20at%2009.49.49%20(1).jpeg)
Pada gambar di atas, pc0 (192.168.4.2) melewati router 2 (192.168.4.1) ke pc1 (192.168.5.2), lalu ke router 1 (192.168.3.2) dan akhirnya ke pc1 (192.168.5.2) Anda dapat melihatnya itu dilacak. ).
![](https://github.com/argarafiar/praktikum-pkj/blob/main/minggu8/asset/WhatsApp%20Image%202022-10-16%20at%2009.52.27.jpeg?raw=true)
Demikian pula, pc1 (192.168.5.2) mencapai pc0 (192.168.4.2) melalui router 1 (192.168.5.1), kemudian router 2 (192.168.3.1), dan akhirnya pc0 (192.168. 4.2).

Anda dapat melihat bahwa jalur yang diambil oleh paket data serupa tetapi tidak sama. Hal ini dikarenakan setiap router memiliki routing yang berbeda-beda. Dalam perutean ini router memilih jalur dengan metrik terendah. Namun, kali ini metrik yang digunakan untuk semua perutean adalah default 10. Jadikan pemilihan jalur kurang sensitif terhadap metrik.

## Mengubah Metric Static Routing
| Device | Destination Network | Netmask | Via | Metric |
| ------ | ------ | ------ | ------ | ------ |
| Router 0	 | 192.168.4.0	 | 255.255.255.0 | 192.168.2.1 | 10 (Default) |
|  | 192.168.5.0 | 255.255.255.0 | 192.168.1.1 | 10 (Default) |
| Router 1 | 192.168.4.0 | 255.255.255.0 | 192.168.3.1 | 10 (Default) |
|  | 192.168.2.0 | 255.255.255.0 | 192.168.1.2 | 10 (Default) |
|  | 192.168.4.0 | 255.255.255.0 | 192.168.1.2 | 1 |
| Router 2 | 192.168.5.0 | 255.255.255.0 | 192.168.3.1 | 10 (Default) |
|  | 192.168.1.0 | 255.255.255.0 | 192.168.2.2 | 10 (Default) |
|  | 192.168.5.0 | 255.255.255.0 | 192.168.2.2 | 1 |
Anda dapat mengubah jalur yang paling efisien dengan mengubah nilai metrik dalam konfigurasi perutean statis. Pada percobaan ini, rute melalui Router 1 merupakan rute yang paling efisien.
![](https://raw.githubusercontent.com/argarafiar/praktikum-pkj/main/minggu8/asset/WhatsApp%20Image%202022-10-16%20at%2010.01.41.jpeg)
Pada gambar di atas, kita dapat melihat bahwa pc0 (192.168.4.2) melacak ke pc1 (192.168.5.2) setelah menambahkan router statis baru dengan metrik 1. Jalur yang ditempuh paket data adalah melalui Router 2 (192.168.4.1) ke Router 0 (192.168.2.2) dan terakhir ke pc1 (192.168.5.2).
![](https://raw.githubusercontent.com/argarafiar/praktikum-pkj/main/minggu8/asset/WhatsApp%20Image%202022-10-16%20at%2010.02.51.jpeg)
Demikian pula, pc1 (192.168.5.2) diteruskan ke pc0 (192.168.4.2). Jalur yang ditempuh paket data adalah melalui Router 1 (102.168.5.1) ke Router 0 (192.168.1.2) dan terakhir ke pc0 (192.168.4.2).

Anda dapat melihat bahwa jalur yang diambil oleh paket data berbeda dari sebelumnya. Hal ini dikarenakan setiap router memiliki routing yang berbeda-beda. Dalam perutean ini router memilih jalur dengan metrik terendah. Oleh karena itu, pemilihan jalur dipengaruhi oleh metrik. Pada percobaan ini jalur yang melalui Router 1 merupakan jalur yang paling efisien. Ini karena perutean melalui router 0 memiliki metrik 1 dan perutean melalui router 1 dan 2 memiliki metrik 10.
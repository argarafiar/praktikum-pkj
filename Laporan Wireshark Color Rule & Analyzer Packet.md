# Laporan Praktikum Konsep Jaringan
## Pewarnaan Paket
| Color | Packet Type |
| ------ | ------ |
| Light Purple | TCP |
| Light Blue | UDP |
| Black | Packets with errors |
| Light green | HTTP traffic |
| Light yellow | Windows-specific traffic, including Server Message Blocks (SMB) and NetBIOS |
| Dark yellow | Routing |
| Dark gray | TCP SYN, FIN and ACK traffic |

Skema pewarnaan default ditunjukkan pada gambar dibawah.
![](https://www.wireshark.org/docs/wsug_html_chunked/wsug_graphics/ws-coloring-rules-dialog.png)

## Check IP Address
![](https://i.ibb.co/ccqScFP/Whats-App-Image-2022-09-03-at-20-41-54.jpg)
Dapat kita ketahui bahwa ip pada laptop saya yakni 192.168.1.8 dan default gatewaynya 192.168.1.8 dengan menggunakan ping pada default gateway yang diberikan oleh router (enp4s0 / ethernet) sudah bisa melakukan analisa suatu packet dengan bantuan Wireshark.

## Detail Packet Analyzer Frame
![](https://i.ibb.co/Z1n1r2L/Whats-App-Image-2022-09-03-at-20-54-18.jpg)
Dalam box frame terdapat:
 - Arrival Time: Sep  3, 2022 20:33:32.666981000 SE Asia Standard Time Menunjukkan waktu saat pengiriman data
 - [Time delta from previous captured frame: 0.002495000 seconds] [Time delta from previous displayed frame: 0.002495000 seconds] [Time since reference or first frame: 14.872848000 seconds] Menunjukkan waktu sebelum capture dari frame, yaitu 0.002495000 seconds, waktu setelah frame ditampilkan yaitu 0.002495000 seconds, dan waktu sejak awal frame 14.872848000 seconds.
 - Frame Number: 919 Menunjukkan nomor dari frame tersebut yaitu 919.
 - Frame Length: 164 bytes (1312 bits) Menunjukkan panjangnya frame adalah sebasar 1312 bits.
 - [Protocols in frame: eth:ethertype:ip:tcp] Menunjukkan protokol-protokol apa saja yang ada di frame 1 yaitu ada Ethernet, Internet Protocol (IP), Internet Control Message Protocol (ICMP) & Data.
 - Kesimpulan: Lapisan ini menunjukkan apa saja yang ada dalam satu frame yaitu seperti protokol-protokol yang ada di lapisan ini Ethernet, Internet Protocol (IP), Transmission Control Protocol (TCP), Hypertext Transfer Protocol (HTTP), dan data-text-lines.

## Detail Packet Analyzer Ethernet II
![](https://i.ibb.co/X812Yvk/Whats-App-Image-2022-09-03-at-21-09-11.jpg)
Dalam box Ethernet II terdapat:
 - Source: zte_56:d1:4e (dc:df:d6:56:d1:4e), Destination: TP-Link_7e:35:5f (b4:b0:24:7e:35:5f) Menunjukkan MAC dari source yaitu zte_56:d1:4e  -  (dc:df:d6:56:d1:4e) dan MAC dari destination TP-Link_7e:35:5f (b4:b0:24:7e:35:5f).
 - Kesimpulan: Lapisan data link MAC dari source yaitu zte_56:d1:4e  -  (dc:df:d6:56:d1:4e) dan MAC dari destination TP-Link_7e:35:5f (b4:b0:24:7e:35:5f).

## Detail Packet Analyzer IPV4
![](https://i.ibb.co/8xxNxfC/Whats-App-Image-2022-09-03-at-21-20-42.jpg)
Dalam box Internet Protocol terdapat:
 - 0100 .... = Version: 4 Menunjukkan IP versi yang digunakan adalah versi 4
.... 0101 = Header Length: 20 bytes (5) Menunjukkan panjangnya header yang ada di lapisan network adalah sebesar 20 bytes
 - Source Address: 192.168.1.6, Destination Address: 192.168.1.8 Menunjukkan IP dari source yaitu 192.168.1.6 dan IP dari destination yaitu 192.168.1.8
 - Kesimpulan: Lapisan network, panjangnya header yang diberikan sebesar 20 bytes dengan IP source 192.168.1.6 dan IP destination yaitu 192.168.1.8

## Protcol TCP
![](https://i.ibb.co/3C3jSSm/Whats-App-Image-2022-09-03-at-21-28-31.jpg)

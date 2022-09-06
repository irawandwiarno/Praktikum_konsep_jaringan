## Color rule di Wireshark
Aturan warna ini untuk menetapkan warna ke daftar perangkat lunak Wireshark sehingga Anda dapat lebih mudah mengidentifikasi jenis paket berdasarkan kode warna. Ada banyak kode warna kode warna yang mewakili jenis kemasan tertentu. Klasifikasi kode warna adalah sebagai berikut:

| Warna      | Jenis Paket |
| ----------- | ----------- |
| Ungu Muda      | TCP       |
| Biru Muda   | UDP        |
| Hitam   | Paket dengan kesalahan        |
| Hijau Muda   | Trafic HTTP        |
| Kuning Muda   | Lalu lintas khusus Windows, termasuk Server Message Blocks (SMB) dan NetBIOS       |
| Kuning Gelap   | Rute        |
| Abu-abu Gelap   | TCP SYN, FIN dan ACK lalu lintas        |

![](https://www.wireshark.org/docs/wsug_html_chunked/wsug_graphics/ws-coloring-rules-dialog.png)

## Penjelasan masing masing packet
### TCP
![TCP](https://i.ibb.co/kSLB4GZ/Screenshot-2022-09-01-172839.png)

|     |     |     |
| --- | --- | --- |
| Nama field | Ukuran | Keterangan |
| Source Port | 2 byte (16 bit) | Menunjukkan sumber protokol lapisan aplikasi yang mengirim segmen TCP yang sesuai. Gabungan antara \_field\_ \*\*Source IP Address\*\* dalam \_header IP\_ dan \_field\_ \*\*Source Port\*\* dalam \_field\_ \_header TCP\_ disebut juga sebagai \*\*\_socket\_ sumber\*\*, yang berarti sebuah alamat global dari mana segmen dikirimkan. Lihat juga port TCP. |
| Destination Port | 2 byte (16 bit) |Menentukan tujuan protokol lapisan aplikasi untuk menerima segmen TCP yang sesuai. Kombinasi bidang alamat IP tujuan header IP dan bidang port tujuan bidang header TCP juga dikenal sebagai \*\*\_socket\_ tujuan\*\*, yang berarti sebuah alamat global ke mana segmen akan dikirimkan. |
| Sequence Number | 4 byte (32 bit) | Menentukan nomor urut dari oktet pertama data dalam segmen TCP yang akan dikirim. Bidang ini harus selalu disetel, meskipun segmen tidak memiliki data (payload). Saat Anda memulai sesi koneksi TCP, segmen dengan bendera SYN (sinkronisasi) diatur ke nilai 1 dan bidang ini berisi nilai nomor urut awal (ISN). Ini berarti bahwa oktet pertama dari aliran byte koneksi adalah ISN+1.|
| Acknowledgment Number | 4 byte (32 bit) | Menentukan nomor urut oktet berikutnya dalam aliran byte yang diharapkan pengirim dari penerima pada pengiriman berikutnya. Nomor pengakuan sangat penting untuk segmen TCP dengan flag ACK diatur ke 1. |
| Data Offset | 4 bit | Menunjukkan posisi awal data dalam segmen TCP. Bidang ini juga bisa berarti ukuran header TCP. Seperti halnya field \*\*Header Length\*\* dalam header IP, field ini merupakan angka dari word 32-bit dalam header TCP. Untuk segmen TCP minimal (tidak ada opsi TCP tambahan), bidang ini disetel ke nilai 0x5. Ini berarti bahwa data segmen TCP dimulai pada oktet ke-20 dari awal segmen TCP. Jika bidang offset data diatur ke 15, yang merupakan nilai maksimum (24=16), panjang header TCP ukuran maksimum adalah hingga 60 byte. |
| Reserved | 6 bit | Direservasikan untuk digunakan pada masa depan. Pengirim segmen TCP akan mengeset bit-bit ini ke dalam nilai 0. |
| Flags | 6 bit | Mengindikasikan flag-flag TCP yang memang ada enam jumlahnya, yang terdiri atas: URG (Urgent), ACK (Acknowledgment), PSH (Push), RST (Reset), SYN (Synchronize), dan FIN (Finish). |
| Window | 2 byte (16 bit) | Menunjukkan jumlah byte yang tersedia di buffer host penerima untuk segmen tertentu. Buffer ini, disebut buffer penerima, digunakan untuk menyimpan aliran byte yang masuk. Dengan menetapkan ukuran jendela untuk setiap segmen, penerima segmen TCP memberi tahu pengirim segmen berapa banyak data yang dapat dikirim dan buffer yang berhasil. Ini untuk memastikan bahwa pengirim segmen tidak mengirim lebih banyak data daripada ukuran buffer penerima. Nilai bidang ini adalah 0 jika buffer penerima penuh. Jika nilainya 0\\, pengirim tidak dapat mengirim lebih banyak segmen ke penerima hingga nilai bidang ini berubah (bukan 0). Tujuan hal ini adalah untuk mengatur lalu lintas data atau \_flow control\_. |
| Checksum | 2 byte (16 bit) | Mampu melakukan pengecekan integritas segmen TCP (\_header\_-nya dan \_payload\_-nya). Nilai field Checksum akan diatur ke nilai 0 selama proses kalkulasi checksum. |
| Urgent Pointer | 2 byte (16 bit) | Menandakan lokasi data yang dianggap “urgent” dalam segmen. |
| Options | 4 byte (32 bit) | Berfungsi sebagai penampung beberapa opsi tambahan TCP. Setiap opsi TCP akan memakan ruangan 32 bit, sehingga ukuran header TCP dapat diindikasikan dengan menggunakan field Data offset. |

### ICMP
![ICMP](https://i.ibb.co/SmYfmLq/Screenshot-2022-09-01-172918.png)
1. Version (4 bit). Menunjukkan format dari internet header. Versi saat ini sebagaimana dijelaskan pada RFC 791 adalah versi 4.
2. Internet header length (IHL: 4 bit). Menjelaskan panjang dari header menggunakan 32-bit word. Ukuran minimum header yang diijinkan adalah 5 word.
3. Type of service / jenis servis (8 bit). Data pada field ini menunjukkan kualitas layanan yang diinginkan.
4. Total Length/panjang keseluruhan (16 bit). Panjang keseluruhan ICMP dalam oktet, termasuk header dan data IP. Field ini memungkinkan datagram berisi sampai 66535 oktet. Standar yang ada menganjurkan tiap host bersiap siap untuk menerima datagram dengan panjang paling tidak 576 oktet.
5. Identification (16 bit). Field identifikasi digunakan untuk membantu proses penggabungan kembali pecahan-pecahan dari sebuah datagram.
6. Flag (3 bit). Field ini berisi tiga control flag.
7. Bit 0. Dicadangkan , harus 0.
8. Bit 1 (DF). 0 = bisa dipecah menjadi fragmen; 1 = tidak boleh dipecah
9. Bit 2 (MF). 0 = fragmen terakhir; 1 = masih ada fragmen lagi.
10. Bila sebuah datagram dipecah, MF bit untuk tiap fragmen kecuali yang terakhir bernilai 1.
11. Fragment Offset / posisi fragmen (13 bit). Untuk datagram yang dipecah, menunjukkan posisi fragmen ini dalam datagram.
12. Time To Live / waktu hidup (8 bit). Menunjukkan waktu maksimum bagi sebuah datagram untuk berada dalam suatu jaringan. Bila field ini memberi nilai 0, datagram akan dibuang. Field ini di modifikasi selama tahap pemrosesan header IP dan umum nya dihitung dalam detik. Namun tiap modul IP yang menangani datagram harus mengurangi Time To Live ini dengan 1. mekanisme ini memastikan bahwa datagram yang tak terkirim suatu saat akan dibuang.
13. Protokol (8 bit). Protokol lapisan atas yang berhubungan dengan bagian data dari datagram.
14. Header checksum (16 bit) Sebuah nilai checksum untuk header saja. Nilai ini harus dihitung ulang tiap kali header dimodifikasi.
15. Source Address (32 bit). Alamat IP dari host yang mengirimkan datagram.
16. Destination Address (32 bit). Alamat IP dari host yang merupakan tujuan akhir datagram.
17. Option (0 sampai 11 32-bit word). Dapat berisi 0 atau lebih pilihan.

### Ethernet II
![Ethernet II](https://i.ibb.co/Jy49hjc/Screenshot-2022-09-01-173003.png)
* Pembukaan - Frame Ethernet dimulai dengan pembukaan 7-byte. Ini adalah pola bolak-balik dari 0 dan 1 yang menandai awal dari sebuah frame dan memungkinkan pengirim dan penerima untuk menyinkronkan bit. Awalnya, PRE (pembukaan) diperkenalkan untuk memungkinkan hilangnya beberapa bit karena penundaan sinyal. Namun, Fast Ethernet saat ini tidak memerlukan pembukaan untuk melindungi frame bit.
PRE (pembukaan) menunjukkan kepada penerima bahwa bingkai akan datang dan memungkinkan penerima untuk menyinkronkan ke aliran data sebelum bingkai yang sebenarnya dimulai.
* Mulai dari Frame Delimiter (SFD) - Ini adalah bidang 1-byte yang selalu disetel ke 10101011. SFD menunjukkan bahwa bit masa depan dimulai dari frame, yang merupakan alamat tujuan. SFD terkadang dianggap sebagai bagian dari PRE. Itu sebabnya pembukaan ditulis sebagai 8 byte di banyak tempat. SFD memperingatkan stasiun bahwa ini adalah kesempatan terakhir mereka untuk melakukan sinkronisasi.
* Destination Address – Ini adalah bidang 6-Byte yang berisi alamat MAC mesin tempat data ditujukan.
* Alamat Sumber - Ini adalah bidang 6-byte yang berisi alamat MAC dari komputer sumber. Alamat sumber selalu merupakan alamat tunggal (unicast), jadi bit paling tidak signifikan dari byte pertama selalu 0.
Panjang - Panjang adalah bidang 2-byte yang menentukan panjang seluruh bingkai Ethernet. Bidang 16-bit ini dapat berisi nilai dengan panjang berapa pun antara 0 dan 65534, tetapi panjangnya tidak boleh lebih dari 1500 karena keterbatasan Ethernet itu sendiri.
* Data - Di sinilah data aktual dimasukkan, juga disebut payload. Saat menggunakan Protokol Internet melalui Ethernet, header IP dan data dimasukkan di sini. Data maksimum yang tersedia adalah 1500 byte. Jika panjang data kurang dari panjang minimum 46 byte, padding nol ditambahkan untuk mencapai panjang minimum yang mungkin.
* Cyclic Redundancy Check (CRC) - CRC adalah bidang 4-byte. Bidang ini berisi kode hash data 32-bit yang dihasilkan dari bidang Alamat Tujuan, Alamat Sumber, Panjang, dan Data. Jika checksum yang dihitung oleh target tidak sesuai dengan nilai checksum yang dikirim, data yang diterima rusak.
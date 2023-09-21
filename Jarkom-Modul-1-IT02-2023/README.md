# Kelompok IT02 #

## Anggota: ##
1. Fathika Afrine Azaruddin (5027211016)
2. Dzakirozaan Uzlahwasata (5027211066)

## Laporan Resmi Modul 1 ##
1. User melakukan berbagai aktivitas dengan menggunakan protokol FTP.
a. Berapakah sequence number (raw) pada packet yang menunjukkan aktivitas tersebut?     
b. Berapakah acknowledge number (raw) pada packet yang menunjukkan aktivitas tersebut?  
c. Berapakah sequence number (raw) pada packet yang menunjukkan response dari aktivitas tersebut?   
d. Berapakah acknowledge number (raw) pada packet yang menunjukkan response dari aktivitas tersebut?
- Gunakan filter untuk memilih paket-paket yang terkait dengan FTP menggunakan filter seperti `ftp`.    
![dokumentasi-soal1](https://i.ibb.co/NTkj8rs/image.png)
- Cari paket yang menunjukkan aktivitas pengunggahan (upload) file. Biasanya, mencakup perintah STOR atau APPE yang digunakan dalam FTP untuk mengunggah file.
- Setelah menemukan paket yang sesuai dengan aktivitas pengunggahan, Anda dapat melihat sequence number (raw) dan acknowledge number (raw) dalam detail paket   
![dokumentasi-soal1](https://i.ibb.co/72mgmFs/image.png)
- Setelah itu kita cari response dari request aktivitas tadi    
![dokumentasi-soal1](https://i.ibb.co/2WD0w6y/image.png)  
- Lalu kita masukan jawaban yang tepat ke terminal dan mendapat flag  
![dokumentasi-soal1](https://i.ibb.co/TKVB6fM/image.png)

2. Sebutkan web server yang digunakan pada portal praktikum Jaringan Komputer!
- Kita perlu menganalisis paket-paket HTTP. Kita dapat melakukan ini dengan mengetikkan "http" dalam kotak pencarian di bagian atas jendela Wireshark.  
![dokumentasi-soal2](https://i.ibb.co/dtpQ30N/image.png)
- Klik pada salah satu paket HTTP dalam daftar hasil pencarian. Di bawah bagian "Hypertext Transfer Protocol", Kita akan melihat informasi tentang server web yang digunakan. Informasi ini akan mencakup nama server dan versi server.
- Lanjutkan dengan mengklik paket-paket HTTP lainnya untuk memastikan bahwa informasi server web yang digunakan konsisten.  
![dokumentasi-soal2](https://i.ibb.co/jDQz1cd/image.png)  
- Lalu kita masukan jawaban yang tepat ke terminal dan mendapat flag    
![dokumentasi-soal2](https://i.ibb.co/Fx7F8cp/image.png)

3. 
A. Berapa banyak paket yang tercapture dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702?
B. Protokol layer transport apa yang digunakan?

- Gunakan filter berikut untuk menemukan paket-paket yang memiliki alamat IP sumber atau tujuan 239.255.255.250 dan port 3702: **ip.addr== 239.255.255.250 &&udp.port == 3702**
- Setelah menerapkan filter ini, Wireshark akan menampilkan hanya paket-paket yang memenuhi kriteria tersebut.
- Lihat jumlah paket yang tercapture setelah menerapkan filter tersebut. Ini akan menjadi jumlah paket yang memiliki IP sumber atau tujuan 239.255.255.250 dan port 3702.
- Untuk menentukan protokol layer transport yang digunakan, Anda dapat melihat jenis protokol pada kolom "Protokol" dalam daftar paket yang terfilter. Protokol ini akan memberitahu Kita apakah UDP atau TCP digunakan dalam komunikasi ini.

![dokumentasi-soal3](https://i.ibb.co/2hD52PD/image.png)

4. Untuk menentukan nilai checksum yang didapat dari header pada paket nomor 130 dalam file pcap, Kita perlu menggunakan perangkat lunak pemrosesan paket seperti Wireshark. Berikut adalah langkah-langkahnya:
   1. Buka file pcap menggunakan Wireshark.
   1. Temukan paket nomor 130 dalam daftar paket. Nomor paket biasanya terlihat di kolom pertama atau kedua dalam daftar paket, tergantung pada tampilan Wireshark yang digunakan.
   1. Klik kanan pada paket nomor 130 dan pilih "Follow" > "TCP Stream" atau "Follow" > "UDP Stream," tergantung pada protokol yang digunakan dalam paket tersebut. Ini akan membuka jendela baru yang menampilkan konten dari paket tersebut.
   1. Dalam jendela stream, Kita akan melihat header paket. Biasanya, nilai checksum akan terdapat dalam bagian header. Nilai checksum dapat ditemukan di dalam paket yang sesuai dengan protokol yang digunakan dalam paket tersebut.
   1. Catat atau salin nilai checksum dari header paket tersebut.
   1. Kita sekarang memiliki nilai checksum dari header pada paket nomor 130.
4. Untuk menjawab pertanyaan-pertanyaan tersebut berdasarkan file pcap yang diberikan, Kita dapat menggunakan perangkat lunak pemrosesan paket seperti Wireshark. Berikut langkah-langkahnya:
1. Buka file pcap menggunakan Wireshark.
2. Untuk mengetahui berapa banyak paket yang berhasil di-capture, Kita dapat melihat jumlah total paket yang terdaftar di bagian bawah jendela Wireshark. Biasanya, Kita akan melihat sesuatu seperti "Displayed: X packets, Captured: Y packets." Jumlah paket yang berhasil di-capture adalah Y.
2. Untuk menemukan port yang digunakan oleh server SMTP, Kita dapat melakukan pencarian menggunakan filter berikut di Wireshark:

**smtp**

Ini akan menampilkan semua paket yang terkait dengan protokol SMTP. Selanjutnya, Kita dapat memeriksa salah satu dari paket ini untuk melihat port tujuan yang digunakan oleh server SMTP. Biasanya, SMTP menggunakan port 25.

4. Untuk menentukan IP yang merupakan public IP, Anda perlu memeriksa alamat-alamat IP yang ada dalam file pcap dan membandingkannya dengan daftar alamat IP publik. Alamat IP publik umumnya adalah alamat yang bukan bagian dari jaringan lokal atau pribadi. Biasanya, alamat IP publik dimulai dengan angka yang tidak termasuk dalam kisaran alamat IP privat seperti 192.168.0.0/16, 172.16.0.0/12, atau 10.0.0.0/8.

![dokumentasi-soal4](https://i.ibb.co/fFJX4w5/image.png)

6. Kode error "server SOURCE ADDRESS 7812 is invalid" yang muncul pada game Valorant terlihat seperti pesan kesalahan yang mengindikasikan bahwa alamat server (SOURCE ADDRESS) dengan nomor 7812 dianggap

tidak valid atau salah. Namun, kode ini mungkin bukan kode kesalahan standar yang digunakan dalam game. **(TIDAKSOLVED)**

7. Untuk menemukan jumlah paket yang menuju alamat IP 184.87.193.88 dalam file pcap, Kita dapat menggunakan perangkat lunak pemrosesan paket seperti Wireshark. Berikut adalah langkah-langkahnya:
1. Buka file pcap menggunakan Wireshark.
1. Gunakan filter berikut untuk menemukan paket-paket yang menuju alamat IP 184.87.193.88:

**ip.dst == 184.87.193.88**

3. Setelah menerapkan filter ini, Wireshark akan menampilkan hanya paket-paket yang memiliki alamat IP tujuan 184.87.193.88.
3. Lihat jumlah paket yang tercapture setelah menerapkan filter tersebut. Ini akan memberikan Kita informasi tentang berapa banyak paket yang menuju ke alamat IP tersebut.

Ini akan memberikan Kita jumlah paket yang menuju alamat IP 184.87.193.88 dalam file pcap yang ada di bawah ini.

![dokumentasi-soal7](https://i.ibb.co/Tvqmsxb/image.png)

![dokumentasi-soal7](https://i.ibb.co/Ptjtvmb/image.png)

8\. Untuk mengatur Wireshark agar hanya menampilkan semua paket protokol yang menuju port 80, Kita dapat menggunakan kueri filter berikut: **tcp.dstport == 80 orudp.dstport == 80**

Filter ini akan memungkinkan Wireshark untuk menampilkan semua paket yang ditujukan ke port 80, baik itu protokol TCP atau UDP. Kemudian, paket-paket akan diurutkan sesuai dengan abjad alamat IP tujuan jika terdapat lebih dari satu alamat yang dituju. Berikut langkah-langkahnya:

1. Buka Wireshark.
1. Pilih antarmuka jaringan yang ingin Kita gunakan untuk memantau lalu lintas.
1. Klik tombol "Mulai" atau "Start" untuk memulai pemantauan lalu lintas.
1. Di bagian atas jendela Wireshark, Kita akan melihat kotak filter yang disebut "Display Filter" atau "Capture Filter." Ketikkan filter berikut ini:

**tcp.dstport == 80 orudp.dstport == 80**

5. Tekan Enter atau klik tombol "Apply" untuk menerapkan filter tersebut.
5. Wireshark akan sekarang hanya menampilkan paket-paket yang ditujukan ke port 80. Jika terdapat lebih dari satu alamat IP tujuan, paket-paket akan diurutkan sesuai dengan abjad.
5. Untuk menghentikan pemantauan, klik tombol "Stop" atau "Berhenti."

Filter ini akan membantu Kita fokus pada lalu lintas yang menuju port 80, yang biasanya digunakan untuk lalu lintas HTTP (web).

9\. Untuk mengatur Wireshark agar hanya menampilkan paket yang berasal dari alamat IP 10.51.40.1 tetapi tidak menuju ke alamat IP 10.39.55.34, Kita dapat menggunakan kueri filter berikut:

**ip.src == 10.51.40.1and ip.dst != 10.39.55.34**

Filter ini akan memungkinkan Wireshark untuk menampilkan hanya paket-paket yang memiliki alamat sumber (source) 10.51.40.1dan alamat tujuan (destination) bukan 10.39.55.34. Berikut adalah langkah-langkahnya:

1. Buka Wireshark dan buka capture file atau mulai memantau lalu lintas pada antarmuka jaringan yang sesuai.
1. Di bagian atas jendela Wireshark, Anda akan melihat kotak filter yang disebut "Display Filter" atau "Capture Filter." Ketikkan filter berikut ini:

**ip.src == 10.51.40.1and ip.dst != 10.39.55.34**

3. Tekan Enter atau klik tombol "Apply" untuk menerapkan filter tersebut.
3. Sekarang, Wireshark hanya akan menampilkan paket-paket yang berasal dari alamat IP 10.51.40.1 dan tidak menuju ke alamat IP 10.39.55.34.
3. Untuk menghentikan pemantauan atau membersihkan filter, klik tombol "Stop"atau "Berhenti"atau hapus filter di kotak filter.

Dengan filter ini, Kita dapat fokus pada paket-paket yang sesuai dengan kriteria yang Anda tentukan, yaitu berasal dari alamat 10.51.40.1dan bukan menuju ke alamat 10.39.55.34.

10\. Ikuti langkah berikut :

1. Buka file pcap no 10
1. Ketikkan telnet untuk memfilter bagian telnet saja
1. Lakukan analyze dengan menggunakan follow TCP stream

![dokumentasi-soal10](https://i.ibb.co/4VVZGHp/image.png)
![dokumentasi-soal10](https://i.ibb.co/G9gSVxw/image.png)

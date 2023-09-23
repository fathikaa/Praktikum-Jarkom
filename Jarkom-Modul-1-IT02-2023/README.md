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

3. Dapin sedang belajar analisis jaringan. Bantulah Dapin untuk mengerjakan soal berikut:    
a. Berapa banyak paket yang tercapture dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702?   
b. Protokol layer transport apa yang digunakan?
- Gunakan filter berikut untuk menemukan paket-paket yang memiliki alamat IP sumber atau tujuan 239.255.255.250 dan port 3702: `ip.addr== 239.255.255.250 &&udp.port == 3702`
- Setelah menerapkan filter ini, Wireshark akan menampilkan hanya paket-paket yang memenuhi kriteria tersebut. 
![dokumentasi-soal3](https://i.ibb.co/kX8KXQy/image.png)
- Lihat jumlah paket yang tercapture setelah menerapkan filter tersebut. Ini akan menjadi jumlah paket yang memiliki IP sumber atau tujuan 239.255.255.250 dan port 3702.
- Untuk menentukan protokol layer transport yang digunakan, Anda dapat melihat jenis protokol pada kolom "Protokol" dalam daftar paket yang terfilter. Protokol ini akan memberitahu Kita apakah UDP atau TCP digunakan dalam komunikasi ini.   
- Lalu kita masukan jawaban yang tepat ke terminal dan mendapat flag
![dokumentasi-soal3](https://i.ibb.co/7YF6gJ5/image.png)

4. Berapa nilai checksum yang didapat dari header pada paket nomor 130?
- Temukan paket nomor 130 dalam daftar paket. Nomor paket biasanya terlihat di kolom pertama atau kedua dalam daftar paket
- Klik pada paket nomor 130
- Kita akan melihat header paket. Biasanya, nilai checksum akan terdapat dalam bagian header. Nilai checksum dapat ditemukan di dalam paket yang sesuai dengan protokol yang digunakan dalam paket tersebut.
![dokumentasi-soal4](https://i.ibb.co/k2C14by/image.png) 
- Lalu kita masukan jawaban yang tepat ke terminal dan mendapat flag 
![dokumentasi-soal4](https://i.ibb.co/DQdhjbs/image.png)

5. Elshe menemukan suatu file packet capture yang menarik. Bantulah elshe untuk menganalisis file packet capture tersebut.
- Klik kanan pada paket yang berisikan pasword dan pilih "Follow" > "TCP Stream". Ini akan membuka jendela baru yang menampilkan konten dari paket tersebut.   
![dokumentasi-soal5](https://i.ibb.co/2gDMb3H/image.png)
- Dalam jendela stream, Kita akan melihat pesan berupa password.
![dokumentasi-soal5](https://i.ibb.co/wpjf8nS/image.png)
- Decode password tersebut ke Base64, lalu kita menemukan password yang dapat kita masukan ke dalam file zip yang diproteksi  
![dokumentasi-soal5](https://i.ibb.co/52rxhL7/image.png) 
- Didalam file zip yang sudah di ekstrak terdapat file txt yang berisikan alamat nc    
a. Berapa banyak packet yang berhasil di capture dari file pcap tersebut?  
b. Port berapakah pada server yang digunakan untuk service SMTP?  
c. Dari semua alamat IP yang tercapture, IP berapakah yang merupakan public IP?  
- Hitung packet yang ada pada file pcap
- Untuk menemukan port yang digunakan oleh server SMTP, Kita dapat melakukan pencarian menggunakan filter `smtp`yang akan menampilkan semua paket yang terkait dengan protokol SMTP.   
- Selanjutnya, Kita dapat memeriksa salah satu dari paket ini untuk melihat port tujuan yang digunakan oleh server SMTP.      
![dokumentasi-soal5](https://i.ibb.co/RjWqyzS/image.png)
- Untuk menentukan IP yang merupakan public IP, Anda perlu memeriksa alamat-alamat IP yang ada dalam file pcap dan membandingkannya dengan daftar alamat IP publik. Alamat IP publik umumnya adalah alamat yang bukan bagian dari jaringan lokal atau pribadi. Biasanya, alamat IP publik dimulai dengan angka yang tidak termasuk dalam kisaran alamat IP privat seperti 192.168.0.0/16, 172.16.0.0/12, atau 10.0.0.0/8.  
- Lalu kita masukan jawaban yang tepat ke terminal dan mendapat flag    
![dokumentasi-soal5](https://i.ibb.co/HV4hKR4/image.png)

7. Berapa jumlah packet yang menuju IP 184.87.193.88?
- Gunakan filter berikut untuk menemukan paket-paket yang menuju alamat IP 184.87.193.88: `ip.dst == 184.87.193.88`  
- Lihat jumlah paket yang tercapture setelah menerapkan filter tersebut    
![dokumentasi-soal7](https://i.ibb.co/HYD1NG0/image.png) 
- Lalu kita masukan jawaban yang tepat ke terminal dan mendapat flag 
![dokumentasi-soal7](https://i.ibb.co/S3NLvsH/image.png) 

8. Berikan kueri filter sehingga wireshark hanya mengambil semua protokol paket yang menuju port 80! (Jika terdapat lebih dari 1 port, maka urutkan sesuai dengan abjad)!  
- Untuk mengatur Wireshark agar hanya menampilkan semua paket protokol yang menuju port 80, Kita dapat menggunakan kueri filter berikut: `tcp.dstport == 80 or udp.dstport == 80`
Filter ini akan memungkinkan Wireshark untuk menampilkan semua paket yang ditujukan ke port 80, baik itu protokol TCP atau UDP. Kemudian, paket-paket akan diurutkan sesuai dengan abjad alamat IP tujuan jika terdapat lebih dari satu alamat yang dituju. 
- Lalu kita masukan jawaban yang tepat ke terminal dan mendapat flag    
![dokumentasi-soal8](https://i.ibb.co/9ZJMYZw/image.png) 

9. Berikan kueri filter sehingga wireshark hanya mengambil paket yang berasal dari alamat 10.51.40.1 tetapi tidak menuju ke alamat 10.39.55.34! 
- Untuk mengatur Wireshark agar hanya menampilkan paket yang berasal dari alamat IP 10.51.40.1 tetapi tidak menuju ke alamat IP 10.39.55.34, Kita dapat menggunakan kueri filter berikut:    
`ip.src == 10.51.40.1 and ip.dst != 10.39.55.34`
   
Filter ini akan memungkinkan Wireshark untuk menampilkan hanya paket-paket yang memiliki alamat sumber (source) 10.51.40.1 dan alamat tujuan (destination) bukan 10.39.55.34. 
- Lalu kita masukan jawaban yang tepat ke terminal dan mendapat flag 
![dokumentasi-soal9](https://i.ibb.co/FY0k6kS/image.png) 

10. Sebutkan kredensial yang benar ketika user mencoba login menggunakan Telnet! 
- Ketikkan telnet untuk memfilter bagian telnet saja  
- Lakukan analyze dengan menggunakan follow TCP stream   
![dokumentasi-soal10](https://i.ibb.co/d6fJLF3/image.png)   
- Lalu kita masukan jawaban yang tepat ke terminal dan mendapat flag    
![dokumentasi-soal10](https://i.ibb.co/jgTkTYs/image.png)
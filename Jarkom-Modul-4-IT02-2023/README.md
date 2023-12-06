# Modul 4 - Kelompok IT02 #

## Anggota: ##
1. Fathika Afrine Azaruddin (5027211016)
2. Dzakirozaan Uzlahwasata (5027211066)

# Laporan Resmi

Disini kami mengimplementasikan ``CIDR`` dengan menggunakan ``Cisco`` dan ``VLSM`` dengan menggunakan ``GNS3``

## Daftar Isi
- [Laporan Resmi](#laporan-resmi)
- [Daftar Isi](#daftar-isi)
  - [Topologi PKT VLSM](#topologi-pkt-vlsm)
  - [Topologi GNS CIDR](#topologi-gns-cidr)
  - [Prefix IP](#prefix-ip)
  - [Rute](#rute)
- [VLSM](#vlsm)
  - [Tree](#tree)
  - [Pembagian IP](#pembagian-ip)
  - [Konfigurasi Network](#konfigurasi-network)
  - [Routing](#routing)
  - [Testing](#testing)
- [CIDR](#cidr)
  - [Penggabungan IP](#penggabungan-ip)
  - [Tree](#tree-1)
  - [Pembagian IP](#pembagian-ip-1)
  - [Testing](#testing-1)

## Topologi PKT VLSM

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/444c2456-6cfa-4b2f-8462-dfd91dd4ed8a)

## Topologi GNS CIDR 

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/d0d71e63-385b-401c-bd61-033df6cb88be)

## Prefix IP 
Kelompok kami memiliki prefix IP `192.234`

## Rute
Setelah melakukan riset dan melakukan percobaan serta melihat cara melakukan routing pada modul [jarkom](https://github.com/arsitektur-jaringan-komputer/Modul-Jarkom/tree/master/Modul-4), diperoleh hasil dari ``rute`` yang kami dapatkan adalah sebagai berikut 

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/d45fc5d0-3d1a-4c59-a2d6-0c7e8c38e98e)

## VLSM
VLSM atau biasa dikenal sebagai *Variable Length Subnet Masking* merupakan teknik ``subnetting`` untuk mengefisienkan pembagian ``IP`` di dalam jaringan. Besar ``netmask`` disesuaikan dengan banyaknya komputer / host yang membutuhkan alamat IP


Dalam suatu subnet. Dengan menggunakan ``VLSM``, kita dapat mengalokasikan blok alamat ``IP`` yang sesuai dengan kebutuhan tiap subnet, tanpa perlu mengikuti batasan-batasan yang seragam. Ini memungkinkan administrator jaringan untuk lebih ``fleksibel`` dalam mengoptimalkan penggunaan alamat ``IP`` dan ``menghindari pemborosan`` sumber daya.

Proses implementasi ``VLSM`` melibatkan ``pemecahan`` suatu jaringan besar ``menjadi subnet yang lebih kecil`` dengan ukuran yang berbeda-beda. Setiap subnet kemudian diberikan ``netmask`` sesuai dengan jumlah host yang diperlukan di dalamnya. Dengan cara ini, subnet yang memiliki lebih banyak host akan mendapatkan ``netmask`` dengan jumlah bit yang lebih sedikit, sementara subnet yang membutuhkan lebih sedikit host akan memiliki ``netmask`` dengan jumlah ``bit`` yang lebih banyak.

Keunggulan utama dari ``VLSM`` adalah ``efisiensi`` penggunaan alamat IP, karena kita dapat menghindari memberikan ``subnet`` dengan ukuran yang besar kepada jaringan kecil yang sebenarnya hanya membutuhkan sejumlah kecil alamat IP. Selain itu, ``VLSM`` juga membantu dalam mengurangi ``konsumsi`` alamat IP secara keseluruhan di dalam jaringan, sehingga dapat ``mendukung pertumbuhan dan perluasan jaringan`` secara lebih efektif.

### Tree
Berikut merupakan hasil ``pemecahan`` subnet besar yang akan dibentuk menjadi ``jaringan`` yang lebih kecil

![tree](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/74a99fc2-9389-477a-9d15-1496380d23d8)

### Pembagian IP
Berikut adalah hasil dari pembagian ``IP`` yang telah kami peroleh dari hasil ``pemecahan`` tadi menjadi jaringan yang lebih kecil

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/9b343a08-b212-439d-91de-c43570f0ff9c)

### Konfigurasi Network

1) Subnetting
   Atur IP interface dari router yang mengarah ke client.
   (Contoh: Subnet A2, Frieren -> Switch3 -> LakeKorridor)
   ![image]
   Atur IP interface dari client yang mengarah ke router.
   (Contoh: Subnet A2, LakeKorridor -> Switch3 -> Frieren)
   ![image]
   ![image]
   (Contoh: Subnet A1, Aura -> Frieren)
   ![image]
   Atur IP interface dari router subnet yang mengarah ke router utama.
   (Contoh: Subnet A1, Frieren -> Aura)
   ![image]
   Lakukan untuk semua subnet.

2) Routing
   Atur default routing dari router subnet ke router utama.
   (Contoh: Frieren -> Aura)
   ![image]
   Atur routing dari router utama ke subnet client.
   (Contoh: Subnet A2, Aura -> Frieren)
   ![image]
   Lakukan untuk semua subnet.

### Testing

Contoh, dilakukan testing dari LakeKorridor ke Aura.
   ![image]
   ![image]

## CIDR
CIDR atau biasa dikenal *Classless Inter-Domain* Routing adalah suatu metode ``pengalamatan dan pengelompokan alamat IP`` yang memungkinkan penggunaan lebih efisien dari ruang alamat IP yang tersedia di Internet. Sebelum diperkenalkannya ``CIDR``, pengalamatan IP didasarkan pada kelas-kelas, seperti ``kelas A, kelas B, dan kelas C``. Setiap kelas memiliki ``ukuran tetap`` untuk jaringan dan host, yang seringkali mengakibatkan pemborosan alamat IP. 

**CIDR** menggantikan ``pendekatan kelas`` dengan memperkenalkan notasi format baru yang memungkinkan ``fleksibilitas`` lebih besar dalam pengelompokan dan alokasi alamat IP. Format notasi CIDR terdiri dari alamat IP dan prefiks (subnet mask) yang diwakili dalam ``format bilangan biner``, seperti contoh berikut:
```
192.234.0.0 / 24
```
Dalam contoh ini, ``"192.234.0.0"`` adalah alamat jaringan, dan ``"/24"`` menunjukkan bahwa ``24 bit pertama`` dari alamat ini digunakan sebagai ``netmask`` (subnet mask). Dengan menggunakan CIDR, ``administrator jaringan`` dapat menentukan ukuran subnet yang sesuai dengan kebutuhan tanpa terikat pada batasan kelas tradisional.

**Keuntungan utama** CIDR melibatkan ``penghematan alamat IP dan pengurangan pemborosan``. Dengan CIDR, tidak perlu lagi mengalokasikan blok alamat IP dengan ukuran yang tetap berdasarkan kelas. Sebagai contoh, jika suatu jaringan ``memerlukan 300 alamat IP``, administrator dapat menggunakan CIDR untuk mengalokasikan subnet dengan panjang netmask yang sesuai tanpa harus memilih kelas yang lebih besar dari yang dibutuhkan.

CIDR juga ``mendukung agregasi rute``, yang memungkinkan penyederhanaan tabel routing di Internet. Dengan ``menggabungkan beberapa blok alamat IP ke dalam satu entri routing``, CIDR membantu mengurangi ukuran tabel routing dan efektif meningkatkan efisiensi dalam pengelolaan lalu lintas jaringan global.

### Penggabungan IP
Berikut merupakan inisialisasi kami yang akan digunakan untuk melakukan penggabungan IP

#### Kondisi Node Awal

![Screenshot 2023-11-28 235649 (2)](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/dd253b5b-c08b-4744-a34f-6102e1a3246d)

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/6f61f095-42d6-47a2-a08c-a1ed24844e6d)

#### Penggabungan Node Pertama (B)

![Screenshot 2023-11-28 235649 (2)](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/57e0463e-3fc7-4f63-a63a-5c009e591fb2)

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/baeebaac-0c5b-4166-8fa8-71b1e4833722)

#### Penggabungan Node Kedua (C)

![Screenshot 2023-11-28 235649 (2)](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/6fbf5677-3fd6-4342-93bc-8e11b8c6e49b)

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/225cabcf-7efc-4eef-bf80-cfd4f3428d78)

#### Penggabungan Node Ketiga

![Screenshot 2023-11-28 235649 (2)](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/8191f2cc-d0df-4f25-ae0f-b9f424c0c487)

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/6b37f0f5-d250-4559-8433-48c55032a19d)

#### Penggabungan Node Keempat

![Screenshot 2023-11-28 235649 (2)](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/156f45cd-22bf-453d-954d-88a8635552c3)

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/d6771785-5559-43d0-821d-36e70432ea6a)

#### Penggabungan Node Kelima

![Screenshot 2023-11-28 235649 (2)](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/4f0ebb94-5288-4390-babb-a749fd63639a)

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/e969aba9-f133-494d-88e5-4cbc7a68e836)

#### Penggabungan Node Keenam

![Screenshot 2023-11-28 235649 (2)](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/776d3727-88d3-4246-856c-288c481b2791)

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/18be64c7-e502-4758-b63a-90d05f3561a1)

#### Penggabungan Node Ketujuh

![Screenshot 2023-11-28 235649 (2)](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/3f7c9c38-2bce-4ae9-ada7-7d2966de1d53)

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/78fa1562-b9dc-4950-87f4-6d34c9a015dc)

#### Penggabungan Node Kedelapan

![Screenshot 2023-11-28 235649 (2)](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/a1afb645-9921-48da-8c50-1101eb0bd3b2)

![image](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/d5794d8e-163a-4b7c-b01c-34f626f7beb6)

### Tree
Setelah dilakukannya ``penggabungan IP``, sekarang kita melakukan pembagian IP dengan menggunakan ``tree`` pada masing-masing kelompok yang telah dibuat sebelumnya sebagai berikut

![tree-CIDR drawio](https://github.com/fathikaa/Praktikum-Jarkom/assets/88912492/d3cdd963-c1e1-42d1-a062-551cf909cbfd)

### Pembagian IP
Berikut merupakan hasil dari pembagian IP berdasarkan Tree yang telah dibuat sebelumnya 

![image](https://github.com/Caknoooo/Jarkom-Modul-3-A09-2023/assets/92671053/1eed8a35-3ae0-4b03-9a3d-cd853c297f9d)

### Testing 

https://github.com/Caknoooo/Jarkom-Modul-4-A09-2023/assets/92671053/b2009280-1257-425d-a359-643e6722b8b6


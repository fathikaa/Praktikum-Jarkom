# Kelompok IT02 #

## Anggota: ##
1. Fathika Afrine Azaruddin (5027211016)
2. Dzakirozaan Uzlahwasata (5027211066)

# Jawaban

## Soal 1 
Sebelum mengerjakan soal ini, kami membuat topologinya sebagai berikut.
![dokumentasi-soal1](https://i.ibb.co/fpsJzDh/Screenshot-2023-10-11-141423.png)

Kemudian kami atur konfigurasi pada setiap node seperti gambar berikut.

a. Pandudewanata sebagai router
![dokumentasi-soal1](https://i.ibb.co/gzJqnhw/Screenshot-2023-10-11-141641.png)
![dokumentasi-soal1](https://i.ibb.co/CPr910L/Screenshot-2023-10-11-141701.png)

b. Nakula sebagai client
![dokumentasi-soal1](https://i.ibb.co/DY2wnW9/Screenshot-2023-10-11-142109.png)

c. Sadewa sebagai client
![dokumentasi-soal1](https://i.ibb.co/jhBZ1BQ/Screenshot-2023-10-11-142147.png)

d. Yudhistira sebagai DNS Master
![dokumentasi-soal1](https://i.ibb.co/dJZ82Hb/Screenshot-2023-10-11-141908.png)

e. Werkudara sebagai DNS Slave
![dokumentasi-soal1](https://i.ibb.co/kSJKRCt/Screenshot-2023-10-11-141759.png)

f. Arjuna sebagai Load Balancer
![dokumentasi-soal1](https://i.ibb.co/84Xmhqn/Screenshot-2023-10-11-142225.png)

g. Abimanyu sebagai Webserver
![dokumentasi-soal1](https://i.ibb.co/GpKrwLM/Screenshot-2023-10-11-142311.png)

h. Prabukusuma sebagai Webserver
![dokumentasi-soal1](https://i.ibb.co/XYTSNv9/Screenshot-2023-10-11-142345.png)

i. Wisanggeni sebagai Webserver
![dokumentasi-soal1](https://i.ibb.co/HpFQWN7/Screenshot-2023-10-11-142424.png)

Setelah itu, setiap node diaktifkan dengan mengklik tombol start. Selanjutnya, menjalankan command ```iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.42.0.0/16``` pada router Foosha upaya dapat terkoneksi dengan internet.

Kemudian pada Yudhistira, Werkudara, dan Nakula dilakukan update package lists dengan menjalankan command:<br>
```apt-get update```

Selanjutnya kami menjalankan command untuk menginstall nano:<br>
```apt-get install nano```

Pada Yudhistira dan Werkudara dilakukan instalasi aplikasi bind9 juga dengan menjalankan command:<br>
```apt-get install bind9 -y```

Pada Nakula dilakukan instalasi dnsutils juga dengan menjalankan command:<br>
```apt-get install dnsutils -y```


## Soal 2 dan 3
Pertama masukan command `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.234.0.0/16` di server yang disambungin ke NAT untuk memberi akses internet untuk semua node. Lalu masukan command `echo nameserver 192.198.122.1 > /etc/resolv.conf` pada semua node yang membutuhkan koneksi internet.

Lalu gunakan command `apt-get update` dan `apt-get install bind9 -y` pada DNSMaster dan DNSSlave. 

### Yudhistira
Setelah itu edit `/etc/bind/named.conf.local` dengan config :


	zone "arjuna.it2.com" {
		        type master;
		        file "/etc/bind/arjuna/arjuna.it2.com";
		};
	
	zone "abimanyu.it2.com" {
			type master;
	    		file "/etc/bind/arjuna/abimanyu.it2.com";
	};


Lalu buat directory /etc/bind/arjuna/arjuna.it2.com dan isi config dengan :

	;
		; BIND data file for local loopback interface
		;
		$TTL    604800
		@       IN      SOA     arjuna.it2.com. root.arjuna.it2.com. (
		                         2    		; Serial
		                         604800         ; Refresh
		                          86400         ; Retry
		                        2419200         ; Expire
		                         604800 )       ; Negative Cache TTL
		;
		@       IN      NS      arjuna.it2.com.
		@       IN      A       192.234.3.2     ; IP Arjuna
		WWW     IN      CNAME   arjuna.it2.com.

Lalu buat directory /etc/bind/arjuna/abimanyu.it2.com dan isi config dengan :

	;
		; BIND data file for local loopback interface
		;
		$TTL    604800
		@       IN      SOA     abimanyu.it2.com. root.abimanyu.it2.com. (
		                         2		; Serial
		                         604800         ; Refresh
		                          86400         ; Retry
		                        2419200         ; Expire
		                         604800 )       ; Negative Cache TTL
		;
		@       IN      NS      abimanyu.it2.com.
		@       IN      A       192.234.3.3     ; IP Yudhistira
		WWW     IN      CNAME   abimanyu.it2.com.

Lalu jalankan `service bind9 restart`

### Werkudara
Edit /etc/bind/named.conf.local
dan isi :

	zone "abimanyu.it2.com" {
		        type slave;
		        masters { 192.234.1.3; };
		        file "/var/lib/bind/abimanyu.it2.com";
		};

run `service bind9 restart`.

#### Test
![dokumentasi-soal2](https://i.ibb.co/y6VjGM7/Screenshot-2023-10-12-160936.png)
![dokumentadi-soal3](https://i.ibb.co/b6vd7mF/Screenshot-2023-10-12-165312.png)

## Soal 4 dan 5

**add bawah ini** kepada `etc/bind/named.conf.local`

	 zone "3.234.192.in-addr.arpa" {
		    type master;
		    file "/etc/bind/arjuna/3.234.192.in-addr.arpa";
		};

Lalu buat directory dan edit `etc/bind/arjuna/3.234.192.in-addr.arpa`. Isi file dengan :

	
		;
		; BIND data file for local loopback interface
		;
		$TTL    604800
		@       IN      SOA     abimanyu.it2.com. root.abimanyu.it2.com. (
		                         2		; Serial
		                         604800         ; Refresh
		                          86400         ; Retry
		                        2419200         ; Expire
		                         604800 )       ; Negative Cache TTL
		;
		@      IN      NS      abimanyu.it2.com.
		3      IN      PTR     abimanyu.it2.com. ; byte ke-4

Kemudian edit /etc/bind/arjuna/abimanyu.it2.com seperti ini :

	;
		; BIND data file for local loopback interface
		;
		$TTL    604800
		@       IN      SOA     abimanyu.d14.com. root.abimanyu.d14.com. (
		                         2022100601;    ; Serial
		                         604800         ; Refresh
		                          86400         ; Retry
		                        2419200         ; Expire
		                         604800 )       ; Negative Cache TTL
		;
		@       IN      NS      abimanyu.it2.com.
		@       IN      A       192.234.3.3
		WWW     IN      CNAME   abimanyu.it2.com.
		parikesit  IN 	A       192.234.3.3     ; IP Abimanyu

Kemudian restart bind
### Testing
![dokumentasi-soal4](https://i.ibb.co/X2myb7S/Screenshot-2023-10-12-171851.png)
![dokumentasi-soal5](https://i.ibb.co/25JPsgQ/Screenshot-2023-10-12-182323.png)

## Soal 6

### Werkudara
Edit file `etc/bind/named.conf.local` dan tambah :

	zone "abimanyu.it2.com" {
	
	    type slave;
	    masters { 192.234.1.3; }; #IP yudhistira
	    file "/var/lib/bind/abimanyu.it2.com";
	
	};
lalu restart bind.

### Yudhistira

Selanjutnya edit file `etc/bind/named.conf.local` dan tambah :

	zone "abimanyu.it2.com" {
	
	    type master;
	    notify yes;
	    also-notify { 192.234.1.2; };
	    allow-transfer { 192.234.1.2; };
	    file "/etc/bind/arjuna/abimanyu.it2.com";
	
	}
	
`Kemudian restart`

### Testing
![dokumentasi-soal6]( )

## Soal 7 dan 8

### Yudhistira

Edit file /etc/bind/arjuna/abimanyu.it2.com seperti ini :

	; BIND data file for local loopback interface
		;
		$TTL    604800
		@       IN      SOA     abimanyu.it2.com. root.abimanyu.it2.com. (
		                         2		; Serial
		                         604800         ; Refresh
		                          86400         ; Retry
		                        2419200         ; Expire
		                         604800 )       ; Negative Cache TTL
		;
		@       IN      NS      abimanyu.it2.com.
		@       IN      A       192.234.3.3     
		www     IN     CNAME    abimanyu.it2.com.
		parikesit IN 	A       192.234.3.3    
		ns1 	IN 	A 	192.234.1.2 	
		baratayuda IN 	NS 	ns1

Kemudian edit /etc/bind/named.conf.options lalu comment `dnssec-validation auto` dan tambah `allow-query{any;}` di bawahnya. Lalu lakukan restart lagi.

### Werkudara 

Lakukan step yang sama pada file /etc/bind/named.conf.options. Kemudian edit file zone dan tambahkan : 

	
	zone "baratayuda.abimanyu.it2.com" {
			        type master;
			        file "/etc/bind/arjuna/baratayuda.abimanyu.it2.com";
			};

Lalu buat directory delegasi /etc/bind/arjuna/baratayuda.abimanyu.it2.com dan edit file tersebut seperti : 

		;
		; BIND data file for local loopback interface
		;
		$TTL    604800
		@       IN      SOA     baratayuda.abimanyu.it2.com. root.baratayuda.abimanyu.it2
		                            2		; Serial
		                         604800         ; Refresh
		                          86400         ; Retry
		                        2419200         ; Expire
		                         604800 )       ; Negative Cache TTL
		;
		@       IN      NS      baratayuda.abimanyu.it2.com.
		@       IN      A       192.234.3.3
		www    IN      CNAME    baratayuda.abimanyu.it2.com.
		rjp 	IN      A       192.234.3.3

Kemudian restart service bind.

### Testing
![dokumentasi-soal7]( )
![dokumentasi-soal8]( )

## Soal 9 dan 10

Buka webserver Abimanyu, Prabukusuma, Wisanggeni. Lalu run command 
`echo nameserver 192.168.122.1 > /etc/resolv.conf` pada ketiga server tsb.
Setelah itu jalankan `apt-get update &&  apt install nginx php php-fpm -y` untuk menginstall nginx.  Setelah installasi selesai, buat directory dengan command 
`mkdir /var/www/arjuna.d14` dan buat file `/var/www/arjuna.it2/index.php` dan isi file tersebut dengan : 

```
<?php
$hostname = gethostname();
$date = date('Y-m-d H:i:s');
$php_version = phpversion();
$username = get_current_user();


echo "Hello World!<br>";
echo "Saya adalah: $username<br>";
echo "Saat ini berada di: $hostname<br>";
echo "Versi PHP yang saya gunakan: $php_version<br>";
echo "Tanggal saat ini: $date<br>";
?>
```
Kemudian buat file /etc/nginx/sites-available/default dan isi file tersebut dengan config berikut :

```
server {
	listen 8001; # sesuaikan dengan web server Abimanyu:8001, Prabukusuma:8002, Wisanggeni:80003

	root /var/www/arjuna.it2;

	index index.php index.html index.htm;
	server_name _;

	location / {
		try_files $uri $uri/ /index.php?$query_string;
	}

	# pass PHP scripts to FastCGI server
	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
	}

	location ~ /\.ht {
		deny all;
	}

	error_log /var/log/nginx/d14_error.log;
	access_log /var/log/nginx/d14_access.log;
}
```
Kemudian jalankan  `service php7.2-fpm start` dan `service nginx restart`. Setelah itu kembali ke Load Balancer Arjuna. Dalam Load Balancer Arjuna edit file `/etc/nginx/sites-available/default` dan isi dengan : 

```
upstream myweb  {
	server 192.234.3.5:8003; #IP Wisanggeni
	server 192.234.3.4:8002; #IP Prabukusuma
	server 192.198.3.3:8001; #IP Abimanyu
}

server {
	listen 80;
	server_name arjuna.it2s.com;

	location / {
		proxy_pass http://myweb;
	}
}
```
Setelah file tersebut terkonfigurasi, jalankan  `service nginx restart` dan `service bind9 restart`.

### Testing
![dokumentasi-soal9]( )
![dokumentasi-soal10]( )

## Soal 11

Edit file /etc/bind/arjuna/abimanyu.it2.conf pada Yudhistira. Kemudian isi file dengan :
```
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.it2.com. root.abimanyu.it2.com. (
                         2		; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.it2.com.
@       IN      A       192.234.3.3     ; IP Abimanyu
www     IN	CNAME	abimanyu.it2.com.
parikesit IN	A	192.234.3.3     ; IP Abimanyu
ns1	IN	A	192.234.1.2 ; IP Werk
baratayuda IN	NS	ns1
```
Selanjutnya pada server abimanyu, jalankan command `echo nameserver 192.168.122.1 > /etc/resolv.conf` untuk menghubungkan dengan internet. Kemudian jalankan `apt-get update` dan `apt-get install apache2` untuk install apache2.   Kemudian jalankan `apt-get install python3-pip` dan `pip3 install gdown` untuk menginstall python3pip dan install gdown untuk mendownload file dari google drive.  Kemudian pergi ke directory  `cd /var/www` dan download zip files. 

Berikut merupakan command yang dijalankan untuk download dan simpan file pada directory tersebut.

- abimanyu.it2.com
```
gdown 1a4V23hwK9S7hQEDEcv9FL14UkkrHc-Zc
unzip abimanyu.yyy.com.zip
rm abimanyu.yyy.com.zip
mv abimanyu.yyy.com abimanyu.it2
```
- parikesit.abimanyu.it2.com
```
gdown 1LdbYntiYVF_NVNgJis1GLCLPEGyIOreS
unzip parikesit.abimanyu.yyy.com.zip
rm parikesit.abimanyu.yyy.com.zip
mv parikesit.abimanyu.yyy.com parikesit.abimanyu.it2
```

- rjp.baratayuda.abimanyu.it2.com
```
gdown 1pPSP7yIR05JhSFG67RVzgkb-VcW9vQO6
unzip rjp.baratayuda.abimanyu.yyy.com.zip
rm rjp.baratayuda.abimanyu.yyy.com.zip
mv rjp.baratayuda.abimanyu.yyy.com rjp.baratayuda.abimanyu.it2
```
Kemudian pada  ``/etc/apache2/sites-available/000-default.conf``  isi dengan :
```
<VirtualHost *:80>
	ServerAdmin webmaster@localhost
	ServerName abimanyu.it2.com
	ServerAlias www.abimanyu.it2.com
	DocumentRoot /var/www/abimanyu.it2
	
	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

### Testing
![dokumentasi-soal11]( )

## Soal 12
Pada server abimanyu, edit file `/var/www/abimanyu.it2/.htaccess`. Isi dengan :
```
RewriteEngine On
RewriteRule ^index\.php/home$ /home [R=301,L]
```
Jalankan command `a2enmod rewrite`. Kemudian edit file `/etc/apache2/sites-available/000-default.conf` dan isi file dengan : 
```
<Directory /var/www/abimanyu.d14>
	Options +Indexes +FollowSymLinks -Multiviews
	AllowOverride All
        Require all granted
</Directory>
```

### Testing
![dokumentasi-soal12]( )

## Soal 13
Edit file `/etc/apache2/sites-available/parikesit.abimanyu.it2.conf` dan isi file dengan :
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName parikisit.abimanyu.d14.com
    DocumentRoot /var/www/parikesit.abimanyu.d14
</VirtualHost>
```
Jalankan command a2ensite parikesit.abimanyu.it2.conf.


## Soal 14
Edit file  `/etc/apache2/sites-available/parikesit.abimanyu.it2.conf` dan isi file dengan : 
```
<VirtualHost *:80>
 	ServerAdmin webmaster@localhost
    	ServerName parikesit.abimanyu.it2.com
    	DocumentRoot /var/www/parikesit.abimanyu.it2

	<Directory /var/www/parikesit.abimanyu.it2/public>
        	Options +Indexes
    	</Directory>

    	<Directory /var/www/parikesit.abimanyu.it2/secret>
       		Options -Indexes
    	</Directory>
</VirtualHost>
```

### Testing
![dokumentasi-soal14]( )

## Soal 15

Edit file `/etc/apache2/sites-available/parikesit.abimanyu.it2.conf` dan isi dengan : 
```
<VirtualHost *:80>
 	ServerAdmin webmaster@localhost
    	ServerName parikesit.abimanyu.it2.com
    	DocumentRoot /var/www/parikesit.abimanyu.it2

	<Directory /var/www/parikesit.abimanyu.it2/public>
        	Options +Indexes
    	</Directory>

    	<Directory /var/www/parikesit.abimanyu.it2/secret>
       		Options -Indexes
    	</Directory>
	
	<Directory /var/www/parikesit.abimanyu.it2/error>
    		Options FollowSymLinks
    		AllowOverride None
    		Require all granted
	</Directory>

	ErrorDocument 404 /error/404.html
	ErrorDocument 403 /error/403.html
</VirtualHost>
```

### Testing
![dokumentasi-soal15]( )

## Soal 16

Edit file `/etc/apache2/sites-available/parikesit.abimanyu.it2.conf` menjadi :
```
<VirtualHost *:80>
 	ServerAdmin webmaster@localhost
    	ServerName parikesit.abimanyu.it2.com
    	DocumentRoot /var/www/parikesit.abimanyu.it2

	<Directory /var/www/parikesit.abimanyu.it2/public>
        	Options +Indexes
    	</Directory>

    	<Directory /var/www/parikesit.abimanyu.it2/secret>
       		Options -Indexes
    	</Directory>
	
	<Directory /var/www/parikesit.abimanyu.it2/error>
    		Options FollowSymLinks
    		AllowOverride None
    		Require all granted
	</Directory>
	
	Alias "/js" "/var/www/parikesit.abimanyu.it2/public/js"

	ErrorDocument 404 /error/404.php
	ErrorDocument 403 /error/403.php
</VirtualHost>
```

### Testing
![dokumentasi-soal16]( )

## Soal 17
#### Steps:
Pergi ke DNS Slave Werkudara untuk setting subdomai rjp ke IP Abimanyu lalu edit file `/etc/bind/arjuna/baratayuda.abimanyu.it2.com` menjadi : 
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.it2.com. root.baratayuda.abimanyu.it2
			    2		; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      baratayuda.abimanyu.it2.com.
@       IN      A       192.234.1.2 ; IP Werkudara
www	IN      CNAME   baratayuda.abimanyu.it2.com.
rjp	IN      A	192.234.3.3 ; IP Abimanyu
```
3. Kemudian, kembali ke Abimanyu dan edit file `/etc/apache2/sites-available/rjp.baratayuda.abimanyu.it2.conf` dan isi menjadi :
```
<VirtualHost *:14000>
    	ServerAdmin webmaster@localhost
	ServerName rjp.baratayuda.abimanyu.it2.com
    	ServerAlias www.rjp.baratayuda.abimanyu.it2.com
   	DocumentRoot /var/www/rjp.baratayuda.abimanyu.it2
</VirtualHost>

<VirtualHost *:14400>
	ServerAdmin webmaster@localhost
	ServerName rjp.baratayuda.abimanyu.it2.com
    	ServerAlias www.rjp.baratayuda.abimanyu.it2.com
   	DocumentRoot /var/www/rjp.baratayuda.abimanyu.it2
</VirtualHost>
```
 Kemudian jalankan `a2ensite rjp.baratayuda.abimanyu.it2.conf`. Setelah itu tambahkan port 14000 dan 14400 ke `/etc/apache2.ports.conf`
```
Listen 14000
Listen 14400
```

## Soal 18

Edit file ` /var/www/rjp.baratayuda.abimanyu.it2/.htaccess` menjadi : 
```
AuthType Basic
AuthName "Authentication Required"
AuthUserFile /etc/apache2/.htpasswd
Require user Wayang
```
Jalankan `htpasswd -c /etc/apache2/.htpasswd Wayang` kemudian akan diprompt buat password, kemudian masukkan "baratayudait2".
Edit file /etc/apache2/sites-available/rjp.baratayuda.abimanyu.it2.conf menjadi : 
```
<VirtualHost *:14000>
	ServerAdmin webmaster@localhost
	ServerName rjp.baratayuda.abimanyu.it2.com
    	ServerAlias www.rjp.baratayuda.abimanyu.it2.com
   	DocumentRoot /var/www/rjp.baratayuda.abimanyu.it2
	
	<Directory /var/www/rjp.baratayuda.abimanyu.it2>
        	Options Indexes FollowSymLinks
        	AllowOverride All
        	Require all granted
    	</Directory>
</VirtualHost>

<VirtualHost *:14400>
	ServerAdmin webmaster@localhost
	ServerName rjp.baratayuda.abimanyu.it2.com
    	ServerAlias www.rjp.baratayuda.abimanyu.it2.com
   	DocumentRoot /var/www/rjp.baratayuda.abimanyu.it2
	
	<Directory /var/www/rjp.baratayuda.abimanyu.it2>
        	Options Indexes FollowSymLinks
        	AllowOverride All
        	Require all granted
    	</Directory>
</VirtualHost>
```

### Testing 
![dokumentasi-soal18]( )

## Soal 19
Pergi ke DNS Master Yudhistira. Lalu edit file  `/etc/bind/abimanyu/abimanyu.it2.com` menjadi 
```
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.it2.com. root.abimanyu.it2.com. (
                         2		; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.it2.com.
@       IN      A       192.234.3.3     ; IP Abimanyu
www     IN	CNAME	abimanyu.it2.com.
parikesit IN	A	192.234.3.3     ; IP Abimanyu
ns1	IN	A	192.234.1.2 	; IP Werkudara
baratayuda IN	NS	ns1
192.198.3.5 IN	CNAME	www.abimanyu.it2.com.
```

## Soal 20
Pergi ke Web Server Abimanyu  lalu edit file ` /var/www/parikesit.abimanyu.it2/.htaccess` menjadi :
```
RewriteEngine On
RewriteRule .*abimanyu.* /abimanyu.png [R,L]
```
3. Kemudian edit file `/etc/apache2/sites-available/parikesit.abimanyu.it2.conf` menjadi : 
```
<VirtualHost *:80>
 	ServerAdmin webmaster@localhost
    	ServerName parikesit.abimanyu.it2.com
    	DocumentRoot /var/www/parikesit.abimanyu.it2

	<Directory /var/www/parikesit.abimanyu.it2/public>
        	Options +Indexes
    	</Directory>

    	<Directory /var/www/parikesit.abimanyu.it2/secret>
       		Options -Indexes
    	</Directory>
	
	<Directory /var/www/parikesit.abimanyu.it2/error>
    		Options FollowSymLinks
    		AllowOverride None
    		Require all granted
	</Directory>
	
	<Directory /var/www/parikesit.abimanyu.it2>
		Options +Indexes +FollowSymLinks -Multiviews
		AllowOverride All
	</Directory>

	Alias "/js" "/var/www/parikesit.abimanyu.it2/public/js"

	ErrorDocument 404 /error/404.php
	ErrorDocument 403 /error/403.php
</VirtualHost>
```

### Testing
![dokumentasi-soal20]( )

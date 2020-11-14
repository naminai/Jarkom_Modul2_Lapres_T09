# Jarkom_Modul2_Lapres_T09
Anggota Kelompok:
- Donny Kurnia Ramadhani     (05311840000004)  
- Muhammad Zulfikar Fauzi    (05311840000012)

---
__(1)__ Membuat website dengan alamat http://semeruyyy.pw  

Pertama, kita edit /etc/bind/named.conf.local di Malang seperti gambar di bawah. Tujuannya adalah untuk membuat zone baru semerut09.pw dengan type master. Kita juga menambahkan perintah also-notify untuk me-notify slave di Mojokerto dan allow-transfer untuk mengarahkan ke IP Probolinggo. 

![no1_zone](https://user-images.githubusercontent.com/61267430/99147335-b6552680-26b2-11eb-8a61-d5fbb7f40f38.PNG)

Kemudian, kita membuat file /etc/bind/shift/semerut09.pw

![no1_semerut09](https://user-images.githubusercontent.com/61267430/99147334-b5bc9000-26b2-11eb-8d8e-1ab927714262.PNG)

Terakhir, kita test pada Client UML dengan ping semerut09.pw

![no1_ping](https://user-images.githubusercontent.com/61267430/99147332-b48b6300-26b2-11eb-979c-da5c0ec46c36.PNG)

__(2)__ Memberikan alias http://www.semeruyyy.pw

Untuk memberikan alias, kita perlu edit file /etc/bind/shift/semerut09.pw lalu menambahkan baris seperti di bawah ini

![no2_config](https://user-images.githubusercontent.com/61267430/99148034-16020080-26b8-11eb-87c2-59489d0f2aeb.PNG)

Lalu, kita test dengan command host -T CNAME www.semerut09.pw pada Client UML.

![no2_cname](https://user-images.githubusercontent.com/61267430/99148033-15696a00-26b8-11eb-91aa-81e67935a9a2.PNG)

Terakhir, kita coba ping www.semerut09.pw pada Client UML.

![no2_ping](https://user-images.githubusercontent.com/61267430/99148035-169a9700-26b8-11eb-8da4-4b325aab2184.PNG)


__(3)__ Membuat Subdomain http://penanjakan.semeruyyy.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO  

Untuk menambahkan subdomain penanjakan.semerut09.pw, kita perlu menambahkan baris di bawah ini pada file /etc/bind/shift/semerut09.pw

![no3_config](https://user-images.githubusercontent.com/61267430/99148133-adffea00-26b8-11eb-9145-0cd1bcd7f725.PNG)

Setelah itu, kita ping penanjakan.semerut09.pw untuk mengetahui apakah sudah mengarah ke IP Probolinggo atau tidak.

![no3_ping](https://user-images.githubusercontent.com/61267430/99148135-ae988080-26b8-11eb-8559-0572279bc51d.PNG)

__(4)__ Membuat Reverse domain untuk domain utama.  

Pertama kita tambahkan baris di bawah ini pada file /etc/bind/named.conf.local untuk menambahkan zone untuk Reverse DNS

![no4_zone](https://user-images.githubusercontent.com/61267430/99148204-08994600-26b9-11eb-8300-0ab1f506656e.PNG)

Kemudian kita membuat file /etc/bind/shift/83.151.10.in-addr.arpa dengan konfigurasi seperti di bawah

![no4_config](https://user-images.githubusercontent.com/61267430/99148200-06cf8280-26b9-11eb-84c7-852b537323b3.PNG)

Kita coba test dengan melakukan ping IP Probolinggo (10.151.83.156)

![no4_ping](https://user-images.githubusercontent.com/61267430/99148201-07681900-26b9-11eb-8647-a9e3a543b959.PNG)

Kita coba test dengan command host -T PTR 10.151.83.156

![no4_PTR](https://user-images.githubusercontent.com/61267430/99148202-0800af80-26b9-11eb-8238-06e48b8bd638.PNG)

__(5)__ Membuat DNS Server Slave pada MOJOKERTO.  

Pertama, kita buat zone baru di UML Mojokerto. Kemudian kita buat type-nya slave sebaga Slave Server dan Master-nya berada di Malang. Server Malang sudah kita kondisikan supaya telah menjadi Master dan me-notify UML Mojokerto, seperti yang telah dijelaskan di Nomor 1.

![no5_zone](https://user-images.githubusercontent.com/61267430/99148385-ee139c80-26b9-11eb-856b-2f5738ae348c.PNG)

Lalu kita edit resolv.conf di Client UML yaitu Gresik untuk seperti gambar di bawah dan menambahkan IP Mojokerto. 

![no5_nameserver](https://user-images.githubusercontent.com/61267430/99148383-ece26f80-26b9-11eb-881d-deb60fbb3563.PNG)

__(6)__ Membuat Subdomain dengan alamat http://gunung.semeruyyy.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO. 

Pertama kita edit file config di /etc/bind/shift/semerut09.pw dan menambahkan baris seperti di bawah, untuk melakukan delegasi ke Mojokerto

![no5_delegasi(ns1)](https://user-images.githubusercontent.com/61267430/99148597-37182080-26bb-11eb-86f7-f0adb1a446a2.PNG)

Lalu, kita buat config file di Mojokerto pada /etc/bind/delegasi/gunung.semerut09.pw seperti di bawah ini

![no5_config](https://user-images.githubusercontent.com/61267430/99148593-35e6f380-26bb-11eb-82fe-c3d8976043d6.PNG)

Tidak lupa kita buat zone seperti di bawah ini 

![no5_zone](https://user-images.githubusercontent.com/61267430/99148598-37b0b700-26bb-11eb-9012-c46cd7057063.PNG)

Lalu kita coba ping gunung.semerut09.pw

![no6_ping](https://user-images.githubusercontent.com/61267430/99148600-38494d80-26bb-11eb-9491-d9b27a3532c2.PNG)

__(7)__ Membuat Subdomain dengan nama http://naik.gunung.semeruyyy.pw, domain ini diarahkan ke IP Server PROBOLINGGO. Setelah selesai membuat keseluruhan domain, kamu diminta untuk segera mengatur web server. 

Kita edit file /etc/bind/delegasi/gunung.semerut09.pw di UML Mojokerto dan menambahkan subdomain naik seperti di bawah ini

![no7_config](https://user-images.githubusercontent.com/61267430/99148988-bc043980-26bd-11eb-8720-c49cc86b0691.PNG)

Kemudian kita cek ping untuk mengecek apakah sudah mengarah ke IP Probolinggo

![no7_ping](https://user-images.githubusercontent.com/61267430/99148989-bd356680-26bd-11eb-970a-eb5e3f405164.PNG)

__(8)__ Membuat Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw. Awalnya web dapat diakses menggunakan alamat http://semeruyyy.pw/index.php/home.

Pertama, kita membuat file config apache di /etc/apache2/sites-available/semerut09.pw. Kita setting dengan ServerName semerut09.pw dan ServerAlias www.semerut09.pw dan Document Root sesuai dengan permintaan pada /var/www/semerut09.pw.  

![no8_sitesavail](https://user-images.githubusercontent.com/61267430/99151467-02619480-26ce-11eb-85c2-1418ac2b8b0a.PNG)

Kemudian pindahkan file semeru yang sudah di unzip dan pindahkan ke /var/www/semerut09.pw. Jika semua step sudah dilakukan, maka ketika kita mengunjungi semerut09.pw pada browser akan terlihat seperti di bawah ini

![no8_ssweb](https://user-images.githubusercontent.com/61267430/99151468-0392c180-26ce-11eb-8d0e-5baebecf3b64.PNG)

__(9)__ Mengaktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home.

Pada awalnya website bisa diakses dengan semerut09.pw/index.php/home

![no9_indexphphome](https://user-images.githubusercontent.com/61267430/99151695-8ff1b400-26cf-11eb-9700-7bde1f8980d9.PNG)

Kemudian buat file htaccess di /var/www/semerut09.pw seperti di bawah ini. Tujuannya adalah meroute ketika ada request ke "home" maka akan dialihkan ke "index.php/home" (jangan lupa mengaktifkan mod_rewrite)

![no9_htaccess](https://user-images.githubusercontent.com/61267430/99151694-8f591d80-26cf-11eb-9fb6-1c57e1871eef.PNG)

Hasilnya akan seperti ini:

![no9_home](https://user-images.githubusercontent.com/61267430/99151692-8cf6c380-26cf-11eb-90b8-ee7a7c79532c.PNG)

__(10)__ Membuat Website http://penanjakan.semeruyyy.pw yang akan digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur folder sebagai berikut:
/var/www/penanjakan.semeruyyy.pw
--> /public/javascripts
--> /public/css
--> /public/images
--> /errors

Kita buat file config di /etc/apache2/sites-available/penanjakan.semerut09.pw dan kita enable dengan a2ensite penanjakan semerut09.pw. Isi file seperti di bawah ini:

![no10_sitesavail](https://user-images.githubusercontent.com/61267430/99151851-87e64400-26d0-11eb-8935-7bfb7570279b.PNG)

__(11)__ Setting pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan. 

Kita edit /etc/apache2/sites-available/penanjakan.semerut09.pw dengan menambahkan Options +Indexes pada directory public dan Options -Indexes di __dalam__ directory public dengan menggunakan public/* 

![no11_config](https://user-images.githubusercontent.com/61267430/99151888-d267c080-26d0-11eb-8cd1-050336266c6e.PNG)

Isi dari directory css

![no11_css](https://user-images.githubusercontent.com/61267430/99151890-d3005700-26d0-11eb-93f1-56760beaff4f.PNG)

Isi dari directory images

![no11_images](https://user-images.githubusercontent.com/61267430/99151892-d4318400-26d0-11eb-822e-f45c47037546.PNG)

Isi dari directory javascript

![no11_javasc](https://user-images.githubusercontent.com/61267430/99151893-d4ca1a80-26d0-11eb-8b1d-8e357a7b127d.PNG)

Isi dari directory public

![no11_public](https://user-images.githubusercontent.com/61267430/99151895-d562b100-26d0-11eb-9fc0-5d608ec989df.PNG)

__(12)__ Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache. 

Kita tambahkan file htaccess pada /var/www/penanjakan.semerut09.pw dengan isi seperti di bawah. Untuk error kita menggunakan command ErrorDocument kode 404 maka akan redirect ke /errors/404.html

![no12_htaccess](https://user-images.githubusercontent.com/61267430/99151948-528e2600-26d1-11eb-9af7-2ab973ba624a.PNG)

Hasil ketika kita sudah menambahkan file htaccess

![no12_weberror](https://user-images.githubusercontent.com/61267430/99151949-5326bc80-26d1-11eb-8d60-58336e554873.PNG)

__(13)__ Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruyyy.pw/js. Untuk web http://gunung.semeruyyy.pw belum dapat dikonfigurasi pada web server karena menunggu pengerjaan website selesai. 

Kita edit /etc/apache2/sites-available/penanjakan.semerut09.pw dan menambahkan command Alias untuk mempersingkat penanjakan.semerut09.pw/public/javascripts menjadi penanjakan.semerut09.pw/js

![no13_config](https://user-images.githubusercontent.com/61267430/99152022-d9430300-26d1-11eb-9d5c-af12a1cb0ff1.PNG)

Hasilnya menjadi seperti ini:

![no13_jsalias](https://user-images.githubusercontent.com/61267430/99152023-d9db9980-26d1-11eb-9039-bae2f0d3af19.PNG)

__(14)__ Sedangkan web http://naik.gunung.semeruyyy.pw sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada /var/www/naik.gunung.semeruyyy.pw. Dikarenakan web http://naik.gunung.semeruyyy.pw bersifat private 

Pertama-tama kita edit /etc/apache2/ports.conf untuk menambahkan supaya kita bisa listen di port 8888 

![no14_portconf](https://user-images.githubusercontent.com/61267430/99152138-7bfb8180-26d2-11eb-8fa8-a124f90ce9ef.PNG)

Kemudian kita edit pada /etc/apache2/sites-available/naik.gunung.semerut09.pw untuk listen pada port 8888 (VirtualHost \*:8888)

![no14_sitesavail](https://user-images.githubusercontent.com/61267430/99152140-7d2cae80-26d2-11eb-8f72-524e42cec1ac.PNG)

Hasilnya akan menjadi seperti ini:

![no14_web](https://user-images.githubusercontent.com/61267430/99152141-7dc54500-26d2-11eb-9826-a8e8e8cbb99e.PNG)

__(15)__ Membuat web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya
aman dan tidak sembarang orang bisa mengaksesnya. 

Pertama kita set up edit /etc/apache2/sites-available/naik.gunung.semerut09.pw dengan menggunakan command

`htpasswd -c /etc/apache2/.htpasswd semeru` dan passwordnya `kuynaikgunung`.

dan menambahkan persiapan autentikasi password:

- AuthType Basic: Basic Authentication

- AuthName "Restricted Content": Nama yang akan ditampilkan ke user ketika masuk ke website

- AuthUserFile /etc/apache2/.htpasswd: Lokasi file htpasswd

- Require valid-user: Yang bisa mengakses resource dalam web hanya valid user yang telah terdaftar

![no15_configauth](https://user-images.githubusercontent.com/61267430/99152338-c29dab80-26d3-11eb-8feb-f742c5a5867b.PNG)

Isi dari .htpasswd:

![no15_htpasswd](https://user-images.githubusercontent.com/61267430/99152340-c3ced880-26d3-11eb-9b43-19063cba087a.PNG)

Hasilnya seperti gambar di bawah ini:

![no15_web](https://user-images.githubusercontent.com/61267430/99152341-c4676f00-26d3-11eb-9f98-28ac8506770d.PNG)

__(16)__ Ketika mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semeruyyy.pw. 

Untuk mengubah IP maka kita ganti pada /etc/apache2/sites-available/default dan menggunakan command `Redirect / http://semerut09.pw` untuk mengubah ketika request masuk ke IP yang mana di-catch di sites-available default, maka akan redirect ke semerut09.pw

![redirectbaby](https://user-images.githubusercontent.com/61267430/99153024-53768600-26d8-11eb-944b-27a94562bb65.png)

__(17)__ Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.

Kita buat file htaccess di /var/www/penanjakan.semerut09/public/images kemudian kita tambahkan rewrite seperti dibawah ini. Dimana ketika ada substring semeru `(.*)semeru(.*)` akan redirect ke semeru.jpg

![no17_htaccess](https://user-images.githubusercontent.com/61267430/99152917-82d8c300-26d7-11eb-9e39-0139a6873ee4.PNG)

Berikut hasilnya ketika mengakses bukansemeruaja.jpg:

![no17_bukansemeruaja](https://user-images.githubusercontent.com/61267430/99152916-810eff80-26d7-11eb-9cc3-9741449a5402.PNG)

Kemudian pada mahameru, tidak redirect ke semeru.jpg:

![no17_mahameru](https://user-images.githubusercontent.com/61267430/99152918-83715980-26d7-11eb-8cac-25a6c6c7f083.PNG)

Kemudian jika kita coba teyvataja atau url sembarang maka akan 404 not found:

![no17_other](https://user-images.githubusercontent.com/61267430/99152919-85d3b380-26d7-11eb-8c85-d7c798efd720.PNG)

Namun jika ada semeru di bagian manapun pada string maka akan redirect ke semeru:

![no17_pokokadasemeru](https://user-images.githubusercontent.com/61267430/99152920-866c4a00-26d7-11eb-84d8-5cc774c98403.PNG)

Lalu untuk semeru sendiri seperti ini:

![no17_semeru](https://user-images.githubusercontent.com/61267430/99152921-879d7700-26d7-11eb-9eab-c9ed12df877f.PNG)


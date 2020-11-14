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

__(8)__ Membuat Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw. Awalnya web dapat diakses menggunakan alamat http://semeruyyy.pw/index.php/home. Karena dirasa alamat urlnya kurang bagus, maka 


__(9)__ Mengaktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home.


__(10)__ Membuat Website http://penanjakan.semeruyyy.pw yang akan digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur folder sebagai berikut:
/var/www/penanjakan.semeruyyy.pw
--> /public/javascripts
--> /public/css
--> /public/images
--> /errors

__(11)__ Setting pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan. 


__(12)__ Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache. 


__(13)__ Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruyyy.pw/js. Untuk web http://gunung.semeruyyy.pw belum dapat dikonfigurasi pada web server karena menunggu pengerjaan website selesai. 


__(14)__ Sedangkan web http://naik.gunung.semeruyyy.pw sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada /var/www/naik.gunung.semeruyyy.pw. Dikarenakan web http://naik.gunung.semeruyyy.pw bersifat private 


__(15)__ Membuat web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya
aman dan tidak sembarang orang bisa mengaksesnya. 


__(16)__ Ketika mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semeruyyy.pw. 


__(17)__ Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.

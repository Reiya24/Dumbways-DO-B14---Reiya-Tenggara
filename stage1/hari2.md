# 1.Perbedaan IP Public dan IP Private

IP Public adalah alamat IP yang digunakan untuk
mengakses ke internet.

IP Private adalah alamat IP yang digunakan hanya
untuk mengakses ke jaringan lokal saja.

# 2. Perbedaan IP static dan dynamic

IP static adalah IP yang alamatnya tidak akan pernah berubah

sedangkan IP dynamic adalah IP yang alamatnya akan berubah setiap waktu

# Deploy aplikasi web server apache menggunakan apt package

Update repository ubuntu untuk memperbarui local package index dengan menggunakan perintah:
```
sudo apt update
```
![image](https://user-images.githubusercontent.com/36489276/201912100-8a8bf2ee-0a64-4da3-8b51-0e563e5d17d9.png)


install package apache 2: 
```
sudo apt install apache2
```
ketika muncul konfirmasi instalasi, ketik y
![image](https://user-images.githubusercontent.com/36489276/201913191-e0117944-6f5f-4cc7-b524-e4789d2d73e8.png)

Setting firewall
Sebelum untuk mengetes apache, kita perlu setting firewall agar apache dapat berjalan dengan baik
Kita perlu aktivasi UFW dengan menggunakan perintah:
```
sudo ufw enable
```
![image](https://user-images.githubusercontent.com/36489276/201920589-ce969cfe-f402-430d-8f8c-3554dd45c1db.png)

check list ufw dengan menggunakan perintah:
```
sudo ufw app list
```
![image](https://user-images.githubusercontent.com/36489276/201913768-1003e39c-20e6-433a-9dc8-6e21662d4d84.png)

Allow apache dengan menggunakan perintah:
```
sudo ufw allow 'Apache'
```
![image](https://user-images.githubusercontent.com/36489276/201917489-39a7dd3c-cffd-476d-bc84-0436098f0417.png)

check status ufw dengan menggunakan perintah:
```
sudo ufw status
```
![image](https://user-images.githubusercontent.com/36489276/201920813-16dfea6f-5422-4984-882b-8cd26d0a47d7.png)

untuk mengecek apakah service apache berjalan, kita bisa menggunakan perintah
```
sudo systemctl status apache2
```
![image](https://user-images.githubusercontent.com/36489276/201921876-949e693a-8751-43da-8635-73391d241457.png)

Kita sendiri dapat menguji apakah layanan apache telah berjalan dengan benar dengan masuk ke url
```
http://alamat_ip_kita
```
Untuk melihat alamat IP kita, kita dapat melihatnya dengan menggunakan perintah
```
hostname -I
```
![image](https://user-images.githubusercontent.com/36489276/201926193-19bbd405-67e6-4dbf-abb4-9bc3082b62ec.png)

Maka, kita coba tes url tersebut pada browser kita, bila berhasil, maka akan muncul
![image](https://user-images.githubusercontent.com/36489276/201926866-172b1318-b44c-4bc0-b46e-e207a7a4550b.png)

Setelah itu, kita buat sebuah direktori dimana direktori tersebut adalah tempat untuk file-file yang akan kita deploy,
kita bisa menggunakan perintah:
```
sudo mkdir /var/www/nama_domain
```
![image](https://user-images.githubusercontent.com/36489276/201931437-44d8f670-561e-4fc1-be76-0d52dcc90199.png)

setelah itu kita butuh untung mengubah ownershipnya ke user kita, dengan menggunakan perintah
```
sudo chown -R $nama_user:$usergrub /var/www/nama_domain
```
selanjutnya, kita buat file sample html, menggunakan text editor nano
```
sudo nano /var/www/reiya/index.html
```
![image](https://user-images.githubusercontent.com/36489276/201945103-912a5825-a535-4809-978e-52dde01bb871.png)

Setelah itu, kita perlu membuat virtual host file dengan menggunakan perintah:
```
sudo nano /etc/apache2/sites-available/nama_domain.conf
```
lalu isikan dengan:
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName nama_domain
    ServerAlias www.nama_domain
    DocumentRoot /var/www/your_domain
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
![image](https://user-images.githubusercontent.com/36489276/201948226-75b44c6b-6de6-4b1f-99f6-c6efab12f8de.png)

setelah itu, mari kita nyalakan filenya dengan menggunakan perintah
```
sudo a2ensite nama_domain.conf
```
![image](https://user-images.githubusercontent.com/36489276/201950543-122491eb-8a3f-4b26-98b0-71142db4bbe6.png)

matikan default site yang terdefinisi di 000-default.conf:
```
sudo a2dissite 000-default.conf
```
![image](https://user-images.githubusercontent.com/36489276/201951061-d9878bf3-95e8-4c2b-a587-2f1a5abef7a1.png)

untuk menerapkan konfigurasi baru, kita perlu mereload apache dengan menggunakan perintah:
```
systemctl reload apache2
```
![image](https://user-images.githubusercontent.com/36489276/201951764-f48803ef-7b69-4909-8c64-e58557a3c73d.png)

Setelah itu, cek apakah ada eror pada konfigurasi dengan menggunakan perintah:
```
sudo apache2ctl configtest
```
![image](https://user-images.githubusercontent.com/36489276/201952185-041cc11e-af1e-4a30-ab71-9ab320344e97.png)
bila muncul output Syntax OK maka tidak ada kesalahan pada file konfigurasi.

Selanjutanya restart apache untuk mengimplementasi perubahan
```
sudo systemctl restart apache2
```
![image](https://user-images.githubusercontent.com/36489276/201952482-2d685776-98bf-4374-870f-e892d01bb1de.png)






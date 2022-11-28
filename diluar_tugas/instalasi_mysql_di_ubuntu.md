# Instalasi Mysql di Ubuntu

Lakukan update dan upgrade package
```
sudo apt update; sudo apt upgrade -y
```
![image](https://user-images.githubusercontent.com/36489276/204156635-bb04f25d-d566-4bf8-89eb-fa176262d885.png)

Lalu install Mysql
```
sudo apt install mysql* -y
```
![image](https://user-images.githubusercontent.com/36489276/204156913-895aa9a3-f662-4854-90bd-7426f5cf5bdb.png)

catatan : kita tidak bisa langsung menggunakan command sudo mysql_secure_installation, Karena akan terjadi recrusive loop pada saat
mengisi form password, penjelasanya dapat anda lihat [disini](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04).
untuk menyelesaikan proses instalasi, kita perlu masuk ke mysql prompt dengan menggunakan perintah:
```
sudo mysql
```
lalu masukan
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Dumbways123[]';
```
![image](https://user-images.githubusercontent.com/36489276/204157264-c9ec0d69-e3dd-4323-9071-9f854203309d.png)
Catatan:
- Ganti Dumbways123[] dengan password yang kalian inginkan.
setelah itu exit
```
exit
```
![image](https://user-images.githubusercontent.com/36489276/204352169-f1cd65f2-730c-417c-9f9b-773540f7612d.png)

lalu jalankan mysql_secure_instalation untuk melanjutkan proses instalasi mysql
```
sudo mysql_secure_installation
```
![image](https://user-images.githubusercontent.com/36489276/204353254-faf0a2b2-4dad-46a5-9650-eb8df586a967.png)

masukan pasword yang telah dibuat
![image](https://user-images.githubusercontent.com/36489276/204353650-f62ff010-9ff9-4396-bb90-c5292fdb1afb.png)

setelah itu, pilih y untuk mengatur setingan password validation
![image](https://user-images.githubusercontent.com/36489276/204354040-0ee22ab1-6464-41db-9638-598c70136b4f.png)

pilih 0 untuk mengatur password validationnya menjadi low (agar password bisa diisi tanpa kombinasi nomor, karakter spesial, dan mixed case)
![image](https://user-images.githubusercontent.com/36489276/204354361-f26e9d52-fdf6-43a1-8903-67f00ae78c98.png)

pilih y untuk mengubah password root, piih n jika ingin menggunakan password root yang lama, saya akan pilih y
![image](https://user-images.githubusercontent.com/36489276/204360314-0cf2ec99-3666-4bd7-9199-14834ba2a296.png)

masukan password yang baru, lalu masukan ulang password baru,  lalu tekan y untuk konfirmasi
![image](https://user-images.githubusercontent.com/36489276/204360529-10c7cdf8-23e0-447f-86fd-42add5d694a9.png)

pilih y untuk menghapus user anonymous
![image](https://user-images.githubusercontent.com/36489276/204360757-70e57da2-f83d-4273-9617-db7399e43c61.png)

pilih n untuk mengizinkan login secara remote
![image](https://user-images.githubusercontent.com/36489276/204361240-8c85c25b-245a-4a06-afa1-3fb14113f703.png)

pilih y untuk menghapus database test
![image](https://user-images.githubusercontent.com/36489276/204361439-44a692a5-c763-4962-b3c2-bbcafbe57cd1.png)

pilih y untuk mereload privilage table
![image](https://user-images.githubusercontent.com/36489276/204361681-3f9ef06a-9c89-4c5d-b51e-3d0e50971cb9.png)



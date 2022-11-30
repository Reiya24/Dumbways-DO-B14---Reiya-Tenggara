# Deploy Aplikasi dumbflix menggunakan database MySQL Menggunakan Cloud Virtual Machine dari IDCloudHost

Kita akan mendeploy aplikasi Dumbflix di dalam sebuah layanan Cloud IDCloudHost, IDCloudHost adalah sebuah layanan cloud computing berbasis Platform as a Service (PaaS), Penjelasan tentang cloud computing
dapat anda lihat [disini](https://github.com/Reiya24/Dumbways-DO-B14---Reiya-Tenggara/blob/main/diluar_tugas/penjelasan_cloud_computing.md)

Daftar terlebih dahulu akun IDCloudHost, bila sudah, masuk ke halaman dashboard https://console.idcloudhost.com
![image](https://user-images.githubusercontent.com/36489276/204774638-11c22c86-72e6-4740-bbef-eac92c0c9394.png)

# Membuat cloud virtual machine
Pada kasus kali ini, Kita akan menggunakan 2 buah virtual machine, virtual machine pertama berfungsi sebagai AppServer Dumbflix itu sendiri,
Virtual machine kedua berfungsi sebagai Web server menggunakan nginx.

klik virtual Machine

![image](https://user-images.githubusercontent.com/36489276/204774845-3aa06871-13fa-4a8e-96c1-7f842fd9e1f3.png)

setelah itu Sesuaikan sistem operasi yang ingin digunakan, lokasi server, ukuran spesifikasi server, username, password, dan nama resource.

pada kasus ini, saya memilih menggunakan sistem operasi ubuntu 20.04, lokasinya berada di singapura, dan saya memilih untuk mengkostumiasi spesifikasi virutal machine saya menggunakan 2 CPU, 2 RAM, dan 20 GB storage (saya menggunakan saldo pribadi). Lalu saya ceklis pada bagian Public IP untuk mendapatkan IP publik, username dan resource name saya sesuaikan dengan nama saya

bila sudah, klik create

![image](https://user-images.githubusercontent.com/36489276/204776936-d4cbb0a8-ad4a-4593-9765-0b51707e5af6.png)

maka, proses pembuatan virtual machine untuk app server dumbflix sedang dibuat, untuk mempercepat proses pembuatan, klik create new resource dan ulangi step sebelumnya, pastikan untuk menggunakan resource name yang berbeda
![image](https://user-images.githubusercontent.com/36489276/204778878-baeba2b5-d54f-4228-bf78-5306fb728336.png)

# Mengakses Virtual Machine secara remote menggunakan SSH tanpa menggunakan password

pada komputer utama kita, kita perlu untuk generate SSH kita terlebih dahulu
```
ssh-keygen
```
output pertama akan meminta lokasi dimana file ssh akan disimpan, input lokasi yang diinginkan
output kedua akan meminta passphrase, saya memilih untuk mengkosongkannya dengan menekan tombol enter
![image](https://user-images.githubusercontent.com/36489276/204795658-5de466bf-09f1-49fd-9249-d73fe8e2d2ce.png)

Setelah file SSH digenerate, kita gunakan ssh-copy-id untuk menaruh file autotentikasi kita ke dalam virtual machine
```
ssh-copy-id -f -i lokasi_file_ssh.pub nama_user@ip_public
```
![image](https://user-images.githubusercontent.com/36489276/204796610-b7f185db-9b6f-4e9b-93aa-6819d6a0de39.png)
input pertama hanya untuk meminta konfirmasi, kita inputkan yes

setelah berhasil, kita akan mencoba mengaksesnya dengan menggunakan
```
ssh -i lokasi_file_ssh username@ip_public
```
![image](https://user-images.githubusercontent.com/36489276/204797843-b97ecf3c-cbcc-4eaf-bfb8-39483087931e.png)

akses ubuntu server menggunakan ssh berhasil, lakukan untuk vm kedua dengan cara yang sama seperti diatas, saya akan menggunakan file ssh yang sama
![image](https://user-images.githubusercontent.com/36489276/204799022-b1d72655-952e-4f06-af24-7f0a2e768b73.png)

jangan lupa untuk selalu melakukan update untuk melakukan pembaruan dari package - package yang tersedia di repostori dan upgrade (opsional) untuk menginstall
semua pembaruan package - package yang tersedia
```
sudo apt update ; sudo apt upgrade -y
```
![image](https://user-images.githubusercontent.com/36489276/204809095-07a47c45-6ce5-4960-b041-c62c07e56489.png)

terkadang, saat kita menjalankan perintah update & upgrade, akan muncul eror seperti
```
Waiting for cache lock: Could not get lock /var/lib/dpkg/lock-frontend. It is held by process 15110 (unattendeWaiting for cache lock: Could not get lock /var/lib/dpkg/lock-frontend. It is held by process 15110 
```

kita cukup gunakan perintah
```
sudo kill -9 15110
```
sesuaikan nomor 15110 dengan nomor yang tertera di output eror


# copy script dari komputer utama ke virtual machine

![image](https://user-images.githubusercontent.com/36489276/204813883-2b38201b-89c9-484b-b2f4-230ba6d830f3.png)

Saya memiliki script di komputer utama kita bernama node_js_installer.sh dan ingin membuat salinannya ke virtual machine saya, langkah pertama adalah kita perlu ubah perizinan file ssh kita menjadi read write, agar tidak menyebabkan eror seperti ini:
![image](https://user-images.githubusercontent.com/36489276/204809800-4b88e47c-2dd4-48d0-841e-97e0196a1037.png)

ubah perizinan file ssh kita ke menggunakan chomd 600 (read write untuk user, group dan yang lainnya tidak memiliki perizinan)
```
sudo chmod 600 nama_file_ssh ; sudo chmod 600 nama_file_ssh.pub
```
![image](https://user-images.githubusercontent.com/36489276/204810842-e4ff19c3-7496-402d-abcf-c4e429a5b989.png)

Setelah berhasil melakukan perizinan file, gunakan command scp untuk melakukan proses penyalinan dari komputer utama kita ke virtual machine
```
scp -i kunci_ssh nama_file username@ip_public:lokasi_hasil_salinan
```
![image](https://user-images.githubusercontent.com/36489276/204811059-5800a325-e34f-4e43-ad0e-ab336ea057f4.png)

jika sudah berada di virtual machine kita, gunakan chmod 700 agar file dapat di eksekusi
```
chmod 700 namafile
```
![image](https://user-images.githubusercontent.com/36489276/204813248-f4502e99-1bd7-4496-acf0-3a405f23c78a.png)

setelah itu, eksekusi filenya
```
./nama_file.sh
```
![image](https://user-images.githubusercontent.com/36489276/204825360-5a4fdcdc-6f85-40ae-8aa7-cf552fb9e7db.png)


# instalasi mysql-server

untuk menginstall mysql-server, gunakan perintah
```
sudo apt install mysql-server -y
```
![image](https://user-images.githubusercontent.com/36489276/204832960-87fdab48-95d2-4d6f-9560-feba3d54766a.png)

setelah itu jalankan mysql dengan sudo
```
sudo mysql
```
![image](https://user-images.githubusercontent.com/36489276/204833489-7104c4b1-0a55-448a-a3dc-265ddc2b9f9a.png)

kita tidak bisa langsung menggunakan command sudo mysql_secure_installation, Karena akan terjadi recrusive loop pada saat mengisi form password, untuk menyelesaikan proses instalasi, kita perlu masuk ke mysql prompt dan perlu menyetel root password secara manual
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'isi_password_sesuai_kebutuhan';
```
![image](https://user-images.githubusercontent.com/36489276/204833819-67e9dcc2-1ecc-4685-8ec8-6f051aaaa570.png)
setelah itu ketik exit
```
exit
```
![image](https://user-images.githubusercontent.com/36489276/204837024-df020607-6c54-4a0b-b04a-7b7dbeb3e8dc.png)

lalu kita baru bisa menjalankan mysql_secure_instalation tanpa memiliki maslah
```
sudo mysql_secure_installation
```
![image](https://user-images.githubusercontent.com/36489276/204837285-7e8aed63-09fd-45ed-81d6-444bd86b8a96.png)

masukan password root yang sebelumnya sudah disetel
![image](https://user-images.githubusercontent.com/36489276/204837405-bb09e8b1-171a-473a-b669-e683f478a7f8.png)

setelah itu, pilih y untuk mengatur setingan password validation 
![image](https://user-images.githubusercontent.com/36489276/204837628-278c4d58-8efc-47ac-b61b-fa75536a7316.png)

pilih 0 untuk mengatur password validationnya menjadi low (agar password bisa diisi tanpa kombinasi nomor, karakter spesial, dan mixed case) 
![image](https://user-images.githubusercontent.com/36489276/204837721-d719c130-1d4b-435b-95a9-d60de6f6a1a3.png)

pilih y untuk mengubah password root, atau input sembarang kata untuk tidak mengubah password root
![image](https://user-images.githubusercontent.com/36489276/204838017-b1ebed12-7553-46b0-bc87-f06df64f3036.png)

pilih y untuk menghapus anonymous user (anonymous user memungkinkan kita untuk masuk ke mysql tanpa mempunyai akun)
![image](https://user-images.githubusercontent.com/36489276/204838482-dbec0b59-b1cc-4573-8d61-f487e82e8440.png)

pilih y untuk mematikan login secara remote
![image](https://user-images.githubusercontent.com/36489276/204840096-4397be36-5ab1-482e-9ffe-5210d78fe406.png)

pilih y untuk menghapus database tes
![image](https://user-images.githubusercontent.com/36489276/204840265-493118f0-ef93-4bc5-8223-b854bbe047e5.png)

pilih y untuk mereload setingan mysql
![image](https://user-images.githubusercontent.com/36489276/204840396-e8bba5a0-0584-47d4-8d02-e4e69a6eb10f.png)

setelah selesai, kita masuk ke mysql prompt menggunakan user root, jalankan
```
sudo mysql -u root -p
```
![image](https://user-images.githubusercontent.com/36489276/204842800-4f57e611-87ec-4241-bb16-8cd7276a53cc.png)

lalu, kita akan membuat user baru menggunakan perintah
```
CREATE USER 'nama_user_baru'@'localhost' IDENTIFIED BY 'inputkan_password';
```
![image](https://user-images.githubusercontent.com/36489276/204849063-7307d3c0-6af3-4c23-8b1a-e62a23515157.png)

setelah itu, kita beri perizinan penuh kepada user baru kita
```
GRANT ALL PRIVILEGES ON * . * TO 'nama_user'@'localhost';
```
![image](https://user-images.githubusercontent.com/36489276/204853210-1c51e5ac-b05d-4a1e-80c4-a5639c36f68d.png)

setelah itu, flush privileges untuk menyimpan semua perubahan
```
FLUSH PRIVILEGES;
```
![image](https://user-images.githubusercontent.com/36489276/204854051-37a59ddf-be12-4fba-9eaf-32c1eea283d4.png)






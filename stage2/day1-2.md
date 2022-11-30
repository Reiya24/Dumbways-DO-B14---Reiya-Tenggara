# Deploy Aplikasi dumbflix menggunakan database MySQL Menggunakan Cloud Virtual Machine dari IDCloudHost

Kita akan mendeploy aplikasi Dumbflix di dalam sebuah layanan Cloud IDCloudHost, IDCloudHost adalah sebuah layanan cloud computing, Penjelasan tentang cloud computing
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








# Pengenalan Cloud Computing

Definisi Cloud Computing

Adalah sebuah aktivitas melakukan komputasi melalu jaringan internet. Contoh umumnya adalah Penggunaan Google Docs, Keep Notes, dan Github, Karena layanan ini memungkinkan kita untuk mengakses data melalui internet.

Jenis - jenis Cloud Computing Berdasarkan bentuk layanannya :

1. Software as a Service (SaaS)
Adalah layanan cloud computing yang sudah siap pakai. Contohnya :
- Google Drive
- Microsoft Office Online

2. Platform as a Service (PaaS)
Adalah layanan cloud computing yang disediakan dalam bentuk platform yang dapat kita gunakan untuk membuat aplikasi di atasnya, Karena Kita dapat menggunakan fitur yang sudah tersedia seperti Sistem operasi, Web Server, Sistem Database. Jadi kita bisa lebih fokus pada pengembangan aplikasi yang kita buat. Contoh dari layanan ini adalah Google App Engine dan Oracle Cloud Platform.

3. Infrastructure as a Service (IaaS)
Adalah layanan cloud computing  yang hanya menyediakan server. Karena itu, kita harus mengurus Sistem Aplikasi, Keamanan, dan komponen komponen lain secara mandiri, namun dengan kelebihan kita bisa kostumisasi sebebas kita. Contoh dari layanan ini adalah Amazon Web Service dan Microsoft Azure.

# Deploy Aplikasi Dumbflix Menggunakan Cloud Virtual Machine dari IDCloudHost

Kita akan mendeploy aplikasi Dumbflix di dalam sebuah layanan Cloud IDCloudHost, IDCloudHost adalah sebuah layanan cloud computing berbasis Platform as a Service (PaaS).

Sebelumnya, Daftar terlebih dahulu akun IDCloudHost, bila sudah, masuk ke halaman dashboard https://console.idcloudhost.com
![image](https://user-images.githubusercontent.com/36489276/204774638-11c22c86-72e6-4740-bbef-eac92c0c9394.png)

# Membuat cloud virtual machine
Pada kasus kali ini, Kita akan menggunakan 2 buah virtual machine, virtual machine pertama berfungsi sebagai AppServer Dumbflix itu sendiri,
Virtual machine kedua berfungsi sebagai Web server menggunakan nginx.

klik virtual Machine

![image](https://user-images.githubusercontent.com/36489276/204774845-3aa06871-13fa-4a8e-96c1-7f842fd9e1f3.png)

setelah itu sesuaikan sistem operasi, lokasi server, ukuran spesifikasi server, username, password, dan nama resource.

pada kasus ini, saya memilih menggunakan sistem operasi ubuntu 20.04, lokasinya berada di singapura, dan saya memilih untuk mengkostumiasi spesifikasi virutal machine saya menggunakan 2 CPU, 2 RAM, dan 20 GB storage (saya menggunakan saldo pribadi). Lalu saya ceklis pada bagian Public IP untuk mendapatkan IP publik, username dan resource name saya sesuaikan dengan nama saya

bila sudah, klik create

![image](https://user-images.githubusercontent.com/36489276/204776936-d4cbb0a8-ad4a-4593-9765-0b51707e5af6.png)

selagi menunggu proses pembuatan virtual machine untuk app server dumbflix sedang dibuat, klik create new resource dan ulangi step sebelumnya, pastikan untuk menggunakan resource name yang berbeda
![image](https://user-images.githubusercontent.com/36489276/204778878-baeba2b5-d54f-4228-bf78-5306fb728336.png)

# Mengakses Virtual Machine secara remote menggunakan SSH tanpa menggunakan password

pada komputer utama kita, kita perlu untuk generate SSH kita terlebih dahulu
```
ssh-keygen
```
output pertama akan meminta lokasi dimana file ssh akan disimpan, input lokasi yang diinginkan.

output kedua akan meminta passphrase, saya memilih untuk mengkosongkannya dengan menekan tombol enter
![image](https://user-images.githubusercontent.com/36489276/204795658-5de466bf-09f1-49fd-9249-d73fe8e2d2ce.png)

otomatis akan ada 2 file baru di direktori tersebut, 1 sebagai kunci ssh, 1 lagi sebagai gembok ssh (bereknektensikan .pub)

Setelah file SSH digenerate, kita gunakan ssh-copy-id untuk menaruh file gembok ssh kita ke dalam virtual machine
```
ssh-copy-id -f -i lokasi_file_gembok_ssh.pub nama_user@ip_publik
```
![image](https://user-images.githubusercontent.com/36489276/204796610-b7f185db-9b6f-4e9b-93aa-6819d6a0de39.png)
input pertama hanya untuk meminta konfirmasi, kita inputkan yes

setelah berhasil, kita akan mencoba mengaksesnya dengan menggunakan
```
ssh -i lokasi_file_kunci_ssh username@ip_public
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
CREATE USER 'nama_user_baru'@'%' IDENTIFIED BY 'isi_password';
```
![image](https://user-images.githubusercontent.com/36489276/205008569-db20695f-2024-485b-aab6-bbdf2b28755f.png)

setelah itu, kita beri perizinan penuh kepada user baru kita
```
GRANT ALL PRIVILEGES ON * . * TO 'nama_user'@'%';
```
![image](https://user-images.githubusercontent.com/36489276/205008680-464c3fdf-8dd0-4b9c-b450-e8c03f3e4466.png)

setelah itu, flush privileges untuk menyimpan semua perubahan
```
FLUSH PRIVILEGES;
```
![image](https://user-images.githubusercontent.com/36489276/204854051-37a59ddf-be12-4fba-9eaf-32c1eea283d4.png)

# registrasi domain di cloudflare
pergi ke halaman [dashboar cloudflare](https://dash.cloudflare.com/)

lalu pilih akun yang ingin digunakan
![image](https://user-images.githubusercontent.com/36489276/204913560-8e65b847-9ab1-4a28-b39d-82fcf4c5dee3.png)

klik domain yang tersedia
![image](https://user-images.githubusercontent.com/36489276/204913625-d76bd010-ae8f-4331-a510-82d8ada23040.png)

pada menu di sebelah kiri, klik dns

![image](https://user-images.githubusercontent.com/36489276/204913886-3411bf71-7f0e-454f-908f-62e98e623a52.png)

klik add record, untuk nama masukan nama domain (domainnya akan menjadi nama.studentdumbways.my.id)
masukan ip publik dari webserver nginx, matikan switch proxy status, lalu klik save
![image](https://user-images.githubusercontent.com/36489276/204914285-802fe775-8cfd-43ef-b358-43327812d5ea.png)

ulangi proses yang sama, namun tambahkan .api sebelum nama domain yang ingin kita buat
![image](https://user-images.githubusercontent.com/36489276/204915598-57bf97b7-b85d-4df5-a9c1-3ae39801dc15.png)



# Clone Frontend dan Backend

clone Dumbflix frontend dan backend menggunakan perintah:
```
git clone https://github.com/dumbwaysdev/dumbflix-frontend ; https://github.com/dumbwaysdev/dumbflix-backend
```
![image](https://user-images.githubusercontent.com/36489276/204882439-0ecb7a5a-cb8f-4e55-8841-a138842018d2.png)

# nginx
gunakarn virtual machine untuk gateway
karena tadi sudah melakukan apt update dan upgrade, langsung install nginx menggunakan
```
sudo apt install nginx -y
```
![image](https://user-images.githubusercontent.com/36489276/204908530-8bc6e256-dd28-41c5-8c71-dd79c448c6f3.png)

cek status nginx apakah sudah berjalan dengan menggunakan perintah
```
sudo systemctl status nginx
```
![image](https://user-images.githubusercontent.com/36489276/204908766-ff85c71c-77b2-47ed-9854-dcd21530a428.png)

untuk menyetel konfigurasi nginx, pergi ke direktori /etc/nginx
```
cd /etc/nginx
```
![image](https://user-images.githubusercontent.com/36489276/204909444-a6a22113-105b-43bf-97bd-de67436bb2dd.png)

saya akan membuat file baru bernama dumbflix yang nanti untuk menyimpan file konfigurasi, jangan lupa untuk gunakan sudo karena kita berada di dalam file system
```
sudo mkdir dumbflix
```
![image](https://user-images.githubusercontent.com/36489276/204910362-6ac63139-40f8-4626-9362-12cb9d27c061.png)

setelah itu, kita buka file nginx.conf dengan text editor sesuai dengan preferensi masing-masing, disini saya akan mencoba menggunakan vim
```
sudo vim nginx.conf
```
![image](https://user-images.githubusercontent.com/36489276/204910627-a2c5806a-de0a-49c4-b4d4-d07f5ef87deb.png)

hapus tanda pagar yang ditandai
![image](https://user-images.githubusercontent.com/36489276/204911220-9d526920-f805-42b4-a095-6f23373e341e.png)

pindah ke baris bawah, lalu
tambahkan direktori file yang kita buat agar nginx dapat mengenali file konfigurasi kita, atau gunakan simbol bintang agar nginx dapat mengenali semua konfigurasi yang ada di dalam file tersebut
```
include /etc/nginx/nama_direktori/*;
```
![image](https://user-images.githubusercontent.com/36489276/204911434-fcb8589e-d3c1-49e9-8efc-6467c3332e4c.png)

untuk mengecek file konfigurasi apakah ada kesalahan syntax/dsb, gunakan perintah
```
sudo nginx -t
```
![image](https://user-images.githubusercontent.com/36489276/204912367-72bffd9d-4160-420f-b6c0-f3ce1af452ab.png)

setelah itu, kita perlu buat 2 file konfigurasi, untuk frontend dan backend, buat file konfigurasi di direktori yang sudah kita buat.

untuk frontend:
```
sudo nano dumbflix/dumbflix_frontend.conf
```
![image](https://user-images.githubusercontent.com/36489276/204984513-adbbbd89-9734-4f44-a15e-3917128efc7a.png)

server name, masukan domain yang sudah kita buat
untuk lokasi, masukan private IP dari appserver dumbflix, tambahkan port 3000 karena dumbflix frontend jalan di port 3000
![image](https://user-images.githubusercontent.com/36489276/204983417-7a597fa6-8271-4fa9-a68f-88f9c34c4b2a.png)

untuk backend:
```
sudo nano dumbflix/dumbflix_backend.conf
```
![image](https://user-images.githubusercontent.com/36489276/204984763-39da0fa5-145e-43ca-9712-4033a43cb2dd.png)

![image](https://user-images.githubusercontent.com/36489276/204985135-a4ccf830-f64c-4c79-9670-b8cb9a59a0fe.png)

seteleah itu, cek syntaxnya kembali apakah untuk mengecek apakah ada kesalahan penulisan
```
sudo nginx -t
```
![image](https://user-images.githubusercontent.com/36489276/204985711-20e48031-745b-40a0-87d9-d0d0991a122e.png)

setelah itu, restart nginx agar webserver mengenali perubahan
```
sudo systemctl restart nginx
```

![image](https://user-images.githubusercontent.com/36489276/204986233-3bb14e26-39fe-4076-95a5-0701130da0d3.png)



# Dumbflix Frontend
gunakan virtual machine untuk appserver
masuk ke direktori dumbflix frontend yang sudah di clone. setelah itu lakukan npm install untuk menginstall semua depedensi yang diperlukan di dumbflix frontend
```
npm install
```
![image](https://user-images.githubusercontent.com/36489276/204901630-c55de53c-962c-4667-aa36-1a584fdeee4d.png)

# Dumbflix backend

masuk ke direktori dumbflix backend yang sudah di clone.
setelah itu, kita akan mencoba menghubungkan ke database, kita perlu atur setingan untuk koneksi ke databasenya
```
nano config/config.json
```
![image](https://user-images.githubusercontent.com/36489276/204884243-12e0547d-a32d-424e-b3a7-5a3505c6b2f7.png)

pada bagian development, sesuaikan username dan password mysql yang sudah kita buat
![image](https://user-images.githubusercontent.com/36489276/204884133-d222f96e-a5a2-499f-b74d-df5703c6463b.png)

lakukan npm install untuk menginstall semua depedensi yang diperlukan di dumbflix backend
```
npm install
```
![image](https://user-images.githubusercontent.com/36489276/204905894-39649860-8a23-403f-bd36-b1d887d4c339.png)

setelah itu perlu konfigurasi domainnya
```
nano src/config/api.js
```
![image](https://user-images.githubusercontent.com/36489276/205011625-db7dbe9b-e25a-4c98-8dab-552bf1d56d5b.png)

ganti localhost ke domain yang kita punya
![image](https://user-images.githubusercontent.com/36489276/205012531-c16b3766-0155-44bb-8c73-db62d7ae4d12.png)

generate script ecosystem pm2 agar proses deployment lebih mudah
```
pm2 ecosystem simple
```
![image](https://user-images.githubusercontent.com/36489276/205013224-fcef11dc-2969-4794-bfdb-2a53c2ad6e7d.png)

lalu edit script konfigurasinya
```
nano ecosystem.config.js
```
![image](https://user-images.githubusercontent.com/36489276/205013609-f4cf48ca-cdda-48aa-9541-ccc83f5b9926.png)

nama disesuaikan, untuk script isikan perintah untuk membuild npm
![image](https://user-images.githubusercontent.com/36489276/205013736-1358ddf9-4edf-40a0-aa78-5fd29d1d54cc.png)

lalu jalankan file ecosystem dengan menggunakan perintah
```
pm2 start
```
![image](https://user-images.githubusercontent.com/36489276/205014213-0a2a643d-7088-4ed6-a9b4-f9e9d649da02.png)




setelah itu, install sequelize-cli untuk meng ekstrak database
```
npm install -g sequelize-cli
```
![image](https://user-images.githubusercontent.com/36489276/204904602-6caf317d-db7a-445b-a711-7e804b68f78f.png)

setelah itu, generate databasenya dengan menggunakan
```
sequelize db:create
```
![image](https://user-images.githubusercontent.com/36489276/204989062-0560e8e4-b3f4-4c4d-af0e-a0e7c449f286.png)

setelah itu, generate _____________
```
sequelize db:migrate
```
![image](https://user-images.githubusercontent.com/36489276/204989331-ed504143-3214-436a-8b59-da94b3a226d8.png)

copy file .env.example dan paste menjadi .env
```
cp .env.example .env
```
![image](https://user-images.githubusercontent.com/36489276/205015488-2cde69de-d53d-4789-9262-5598828824c9.png)


generate script pm2 agar mudah dijalankan
```
pm2 ecosystem simple
```
![image](https://user-images.githubusercontent.com/36489276/205010031-0a12d7d7-c267-41e0-b50d-a8654ba9d1d5.png)

buka file ecosystemnya
```
nano ecosystem.config.js
```
![image](https://user-images.githubusercontent.com/36489276/205016044-cfff7e2f-cc0d-43c4-ae95-8a3226ba7ccd.png)

jalankan pm2
```
pm2 start
```
![image](https://user-images.githubusercontent.com/36489276/205017604-1cdbc753-93c5-4036-80ea-c0a74ab15d4d.png)

# Menambahkan SSL Menggunakan certbot (wildcard)

pada virtual machine webserver nginx
lakukan proses update pada snap agar mendapatkan versi terbaru dari snapd
```
sudo snap install core; sudo snap refresh core
```
![image](https://user-images.githubusercontent.com/36489276/205045250-783b4eb6-afda-4745-9970-cdbc8107cbed.png)

install certbot menggunakan snap
```
sudo snap install --classic certbot
```
![image](https://user-images.githubusercontent.com/36489276/205045770-21bdd04d-6dae-434e-8a79-d71e4711594a.png)

tambahkan path certbot agar perintah certbot dapat dijalankan
```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
![image](https://user-images.githubusercontent.com/36489276/205046033-7a2ed284-15c9-4e85-9ee7-9a136fe40381.png)

```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
![image](https://user-images.githubusercontent.com/36489276/205046697-8abcf05d-4b10-428a-8f96-dc6e4e9193a8.png)


?????????
```
sudo snap set certbot trust-plugin-with-root=ok
```
![image](https://user-images.githubusercontent.com/36489276/205047942-ef3c4b3b-bd1b-488d-b1cd-cea91fd6303c.png)

install certbot dns plugin
```
sudo snap install certbot-dns-nama_dns_provider
```
![image](https://user-images.githubusercontent.com/36489276/205048978-56788496-8805-4ce1-a1be-7a3a623f2b9c.png)

saya akan menyimpan sebuah file yang berisi API token, saya akan menyimpannya di direktori /root/.my_config/nama_file.ini. karena berada di direktori root
saya mengubah user sebagai root dengan menggunakan
```
sudo su
```
![image](https://user-images.githubusercontent.com/36489276/205052856-025328dc-7583-4cc4-9b60-e047de3918fd.png)

masuk ke folder root dan buat file rahasia
![image](https://user-images.githubusercontent.com/36489276/205053524-d21ddee5-d854-402c-9057-9c81ecf4b1e9.png)

atur perizinan folder yang menampung isi file api token kita menjadi 0700
```
sudo chmod 0700 nama_folder
```
![image](https://user-images.githubusercontent.com/36489276/205078214-ea5b8f94-abd4-4dc8-983b-770d3d40d7eb.png)

buka file yang berfungsi untuk menyimpan API token tadi menggunakan text editor
tambahkan
```
dns_cloudflare_email = "nama_email@nama_email.com"
dns_cloudflare_api_key = "nomor_api_token"
```
![image](https://user-images.githubusercontent.com/36489276/205056553-c4a5ecc0-8eb5-4402-abe5-f3468827f3ce.png)

untuk mengambil global token, pergi ke [dashboard cloudflare](https://dash.cloudflare.com)

lalu klik icon pencarian, lalu ketik api tokens
![image](https://user-images.githubusercontent.com/36489276/205079417-42046246-b21d-4d28-9208-42d1f990f15a.png)

view global API key, dan masukan password
![image](https://user-images.githubusercontent.com/36489276/205080027-55d13e85-f36f-45d4-a5b2-ce1b2b22e7aa.png)



atur perizinan script file menjadi 0400
```
chmod 0400 nama_file
```
![image](https://user-images.githubusercontent.com/36489276/205078334-e62da565-6a05-431c-bcf9-73263a316bd9.png)

setelah itu, jalankan certbot
```
certbot -i nginx \
  --dns-cloudflare \
  --dns-cloudflare-credentials lokasi_API-key \
  -d domain_yang_ingin_didaftarkan \
  -d domain_yang_ingin_didaftarkan \
```
![image](https://user-images.githubusercontent.com/36489276/205085023-20dbf7b9-eac0-4561-a00c-d07f217e1a6b.png)

masukan email untuk mendapatkan pemberitahuan dari certbot

kita harus setuju dengan syarat dan ketentuan, pilih y
![image](https://user-images.githubusercontent.com/36489276/205107120-1183febf-e705-4140-aa86-1b8fe934b6d1.png)

pilih n
![image](https://user-images.githubusercontent.com/36489276/205107159-7dce35c6-43c2-4d7b-8f30-39578a293d41.png)

![image](https://user-images.githubusercontent.com/36489276/205107324-30d321c3-860d-409a-bd21-c27d6f656e8a.png)

# Cek website dumflix apakah sudah berhasil
![image](https://user-images.githubusercontent.com/36489276/205109235-d932bc8e-16c3-4eb5-b231-b0889102c0a4.png)


# 1. Perbandingan antara Monolith & Microservices
-Arsitektur Monolith merupakan sebuah arsitektur dimana semua komponen berada di dalam satu kesatuan yang sama, karena itu proses pengembangan jauh lebih mudah,
Karena berada dalam satu server, dengan begitu juga, latency komunikasinya antar komponen jauh lebih cepat, Namun arsitektur ini juga memiliki beberapa konsekuensi,
karena semua komponen berada di dalam server yang sama, bila terjadi pemeliharanan atau sedang terjadi masalah, Semua komponen tersebut tidak akan berjalan karena
semuanya berada di dalam satu server. Serta arsitektur ini juga memiliki keterbatasan dalam scaling, dimana kita hanya bisa menduplikasi secara keseluran komponen tersebut.

-Sedangkan arsitektur Microserves adalah kebalikannya dari arsitektur monolith, dimana suatu kesatuan tersebut dipecah ke dalam infrastrukturnya sendiri-sendiri, dengan begitu proses Scalingnya bisa lebih fleksibel, Serta jika terjadi proses pemeliharaan atau sedang terjadi masalah, hanya suatu komponen saja yang down, 
komponen komponen lainnya masih bisa bekerja karena terpisah dengan komponen yang sedang down, namun tetap memiliki kekurangan diantaranya proses pengembangannya
jauh lebih rumit karena memiliki arsitektur yang kompleks, serta butuh biaya yang lebih tinggi dibandingkan arsitektur monolith


# 2. Deploy Aplikasi wayshub-frontend menggunakan Node.js
Langkah pertama, kita perlu mengisntall sebuah tool yang berfungsi untuk mengunduh dan menginstal Node.js, yaitu nvm (Node version Manager).
kita dapat menggunakan perintah:
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
![image](https://user-images.githubusercontent.com/36489276/202117375-f4be4e28-9308-4036-b371-5cc3a06624b1.png)

lalu ketikan perintah exec bash untuk melakukan soft restart ubuntu:
```
exec bash
```
![image](https://user-images.githubusercontent.com/36489276/202118095-30d7988a-f299-4689-ab1c-2853e1d6d153.png)

Kita dapat melihat semua versi node.js yang tersedia di nvm dengan menggunakan perintah:
```
nvm list-remote
```
![image](https://user-images.githubusercontent.com/36489276/202146614-b37150b3-3d29-4fff-a2c1-fce5136510d7.png)


Pada kasus ini, kita akan menggunakan Node.Js versi 16 terbaru, kita dapat mengetikan perintah:
```
nvm install 16
```
![image](https://user-images.githubusercontent.com/36489276/202118541-fe4fdef8-c4a5-488e-98a5-d31c89395ffd.png)

Secara default kita seharusnya langsung menggunakan nvm 16, Tapi jika anda berada dalam nvm versi lain dan ingin berpindah menggunakan nvm versi 16
 kita dapat menggunakan perintah:
```
nvm use 16
```
![image](https://user-images.githubusercontent.com/36489276/202118929-a63cc88f-07dc-4fd4-be33-933a0ea797ac.png)

Sebelum melanjutkan ke step selanjutnya, kita perlu berkenalan terlebih dahulu dengan npm (node package manager), Npm merukakan sebuah package manager, namun lebih difokuskan untuk mkebutuhan instalasi depensi untuk Node.Js

untuk mengecek versi nvm, kita dapat mengetikan perintah:
```
nvm -v
```
untuk mengecek versi Node.Js, kita dapat mengetikan perintah:
```
node -v
```
untuk mengecek versi npm, kita dapat mengetikan perintah:
```
npm -v
```
![image](https://user-images.githubusercontent.com/36489276/202150101-335eea80-aee7-4cd1-ace2-e62ef9d33d15.png)

Pada kasus kali ini, karena kita akan mendeploy aplikasi yang sudah ada di dalam repository github, kita perlu melakukan proses cloning terlebih dahulu menggunakan perintah
```
git clone  https://github.com/dumbwaysdev/wayshub-frontend
```
Ganti link tersebut sesuai dengan kebutuhan anda

setelah proses cloning berhasil, kita perlu masuk ke direktori yang sudah kita unduh
![image](https://user-images.githubusercontent.com/36489276/202155373-835493f6-a5f4-4e0c-8aeb-fe418c2501d5.png)

untuk menampahkan package depensi, kita bisa mengetikan perintah:
```
npm install
```
![image](https://user-images.githubusercontent.com/36489276/202156840-c541438d-da40-4235-ae4a-20c75ee7cc3f.png)

kita akan mendeploy aplikasi kita menggunakan pm2, maka sebelum itu, kita harus menginstallnya terlebih dahulu kita dapat menginstallnya melalui npm, cukup ketikan perintah
```
npm install pm2 --location=global 
```
![image](https://user-images.githubusercontent.com/36489276/202217961-d75ea8a0-66ff-4eea-b8db-3d1693688857.png)

setelah itu, kita akan menjalankan npm start di atas pm2, kita bisa mengetikan perintah
```
pm2 start npm -- start
```
![image](https://user-images.githubusercontent.com/36489276/202219313-1f0e6927-2e79-476c-8b05-845b7e16f4e3.png)

setelah itu, kita akan mendeploy dengan menggunakan localtunnel, bila localtunnel belum terinstal, kita bisa menginstallnya dengan mengetikan perintah:
```
npm install -g localtunnel
```
![image](https://user-images.githubusercontent.com/36489276/202157799-b7ac4eeb-c1e0-456c-8dee-fb7cb59030a7.png)

setelah itu, jalankan localtunnel di port 3000
```
lt --port 3000
```
![image](https://user-images.githubusercontent.com/36489276/202219822-c3459973-7e93-4e0f-837b-e2381007c563.png)

langkah terakhir, untuk mengecek apakah sudah terdeploy dengan benar, kita copy kan urlnya, lalu paste di web browser
![image](https://user-images.githubusercontent.com/36489276/202220727-25f55152-d811-425b-a478-49f0c6638a44.png)

# 3. Deploy aplikasi go lang

Pertama tama, kita perlu menginstall go nya itu sendiri, sebenarnya package go sendiri bisa kita install menggunakan package manager bawaan ubuntu sendiri yaitu apt,
hanya perlu mengetikan perintah:
```
sudo apt install golang-go
```
![image](https://user-images.githubusercontent.com/36489276/202230807-68e51e6b-0d35-4be9-88e1-4080210f40b8.png)

otomatis golang akan terinstall dengan versi terbarunya yang tersedia di apt manager, serta environtmentnya pun akan ditambahkan secara otomatis
namun untuk kasus kali ini, kita akan menginstall go lang dengan mengunduhnya secara manual.

langkah pertama, kita unduh terlebih dahulu file binary go nya, kita akan gunakan command wget:
```
wget https://golang.org/dl/go1.16.5.linux-amd64.tar.gz
```
![image](https://user-images.githubusercontent.com/36489276/202233797-f3e4e165-0e14-4d6c-b184-f761353945db.png)

untuk berjaga jaga bila direktori golang sudah terisi, kita akan menghapus direktori tersebut dengan menggunakan perintah rm -rf, jangan lupa gunakan sudo karena letak direktori tersebut berada di system
```
sudo rm -rf /usr/local/go
```
![image](https://user-images.githubusercontent.com/36489276/202234378-39122cd5-609f-494e-bc41-e303c0f71619.png)

setelah itu kita kita extrak file binary yang sudah kita unduh menggunakan wget, lalu pindahkan ke direktori go
```
sudo tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz
```
![image](https://user-images.githubusercontent.com/36489276/202234616-3c8a1e02-c8ea-46c9-9317-a108162a30ac.png)


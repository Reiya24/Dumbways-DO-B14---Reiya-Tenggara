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

Secara default kita seharusnya langsung menggunakan nvm 16, Tapi jika kita berada dalam nvm versi lain dan ingin berpindah menggunakan nvm versi 16
 kita dapat menggunakan perintah:
```
nvm use 16
```
![image](https://user-images.githubusercontent.com/36489276/202118929-a63cc88f-07dc-4fd4-be33-933a0ea797ac.png)

Sebelum melanjutkan ke step selanjutnya, kita perlu berkenalan terlebih dahulu dengan npm (node package manager), Npm merukakan sebuah package manager, namun lebih difokuskan untuk kebutuhan instalasi depensi untuk Node.Js

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

untuk menambahkan package depensi yang diperlukan, kita bisa mengetikan perintah:
```
npm install
```
![image](https://user-images.githubusercontent.com/36489276/202156840-c541438d-da40-4235-ae4a-20c75ee7cc3f.png)

kita akan mendeploy aplikasi kita menggunakan pm2, maka sebelum itu, kita harus menginstallnya terlebih dahulu kita dapat menginstallnya melalui npm, cukup ketikan perintah
```
npm install pm2 --location=global 
```
![image](https://user-images.githubusercontent.com/36489276/202217961-d75ea8a0-66ff-4eea-b8db-3d1693688857.png)

setelah itu, kita akan menjalankan npm diatas pm2
```
pm2 start npm -- start
```
![image](https://user-images.githubusercontent.com/36489276/202541511-5bf034f7-7e35-4a6f-b281-0971a3540303.png)

jika berjalan dengan benar, maka akan muncul tampilan website sebagai berikut
![image](https://user-images.githubusercontent.com/36489276/202541928-5d32afc2-4378-4447-8981-708cdf31c0a9.png)



# 3. Deploy aplikasi menggunakan go lang

Pertama tama, kita perlu menginstall bahasa go nya itu sendiri, sebenarnya package go sendiri bisa kita install menggunakan package manager bawaan ubuntu sendiri yaitu apt,
hanya perlu mengetikan perintah:
```
sudo apt install golang-go
```
![image](https://user-images.githubusercontent.com/36489276/202230807-68e51e6b-0d35-4be9-88e1-4080210f40b8.png)

otomatis golang akan terinstall dengan versi terbarunya yang tersedia di apt manager, serta environtmentnya pun akan ditambahkan secara otomatis,
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

setelah itu, kita perlu atur path  agar golang bisa dijalankan di direktori manapun kita berada, kita menyimpan path tersebut biasanya di file yang bernama .bashrc
untuk mencari dimana file tersebut berada, kita bisa mencarinya dengan menggunakan perintah:
```
find ~  -maxdepth 1  -name '.bashrc'
```
![image](https://user-images.githubusercontent.com/36489276/202237201-06278ff8-096d-4280-9637-e6f888f90339.png)

setelah ditemukan, kita edit file tersebut menggunakan text editor nano
```
 nano /home/ubuntu/.bashrc
```
![image](https://user-images.githubusercontent.com/36489276/202238568-fcbe977a-df5c-4687-919a-b7b0eb39f278.png)

letakan path di baris manapun, pada kasus ini saya akan di baris terakhir
```
export PATH=$PATH:/usr/local/go/bin
```
![image](https://user-images.githubusercontent.com/36489276/202240049-675bf50c-734c-4f8b-8d1e-73e020e5e324.png)

setelah itu, kita perlu refresh file bashrc tersebut, dengan menggunakan command
```
source /home/ubuntu/.bashrc
```
![image](https://user-images.githubusercontent.com/36489276/202240576-6ded1be3-7ce9-453c-9850-ca3f7b6b5215.png)

kita cek apakah go lang sudah terinstall dengan benar, kita bisa cek saja versi golang tersebut dengan menggunakan command
```
go version
```
![image](https://user-images.githubusercontent.com/36489276/202241304-e8dad3af-788d-42ee-8be1-18daafd2dd02.png)

bila muncul output tersebut, artinya golang telah terinstall dengan benar

selanjutanya, mari kita membuat aplikasi golang sederhana, buat file dengan berekstensikan .go, pada kasus ini saya akan buat filenya dengan nama sayMyName.go
```
nano sayMyName.go
```
![image](https://user-images.githubusercontent.com/36489276/202244342-d3781e0a-9b9d-4bc0-bdb8-213d7f630550.png)

kita isikan
```
package main

import "fmt"

func main() {
    fmt.Println("Reiya Tenggara")
}
```
![image](https://user-images.githubusercontent.com/36489276/202244751-07fa3854-b9b5-4ce5-bcdc-9cfe35632b60.png)

kita bisa menjalankanya dengan menggunakan perintah:
```
go run sayMyName.go
```
![image](https://user-images.githubusercontent.com/36489276/202245270-cd0decd9-e301-45f5-b866-81374035bbd3.png)

kita bisa build agar file tersebut bisa di eksekusi secara cepat menggunakan perintah:
```
go build sayMyName.go
```
![image](https://user-images.githubusercontent.com/36489276/202245708-8c85e63c-c44e-4b6f-a764-81a9bcf267f3.png)

setelah itu kita bisa eksekusi dengan menggunakan perintah:
```
./sayMyName
```
![image](https://user-images.githubusercontent.com/36489276/202246021-5c1466b7-82b8-4c2d-894e-9feba8dfa9aa.png)

jika ingin mengeksekusi dengan menggunakan PM2, kita harus membuat file myName menjadi executable, dengan menggunakan perintah
```
sudo chmod +x sayMyName
```
![image](https://user-images.githubusercontent.com/36489276/202251933-38b2e365-4107-4cc0-b176-75c8dbdd2e59.png)

setelah itu jalankan script executablenya menggunakan pm2
```
pm2 start sayMyName
```
![image](https://user-images.githubusercontent.com/36489276/202546877-c0f8c8a3-fa43-4849-8ab9-cbb134216bbc.png)

# 3. Deploy aplikasi python

python3 sendiri sudah terinstal secara default di ubuntu, jadi kita hanya akan melakukan proses update & upgrade pada apt package manager agar bisa mendapatkan python versi terbaru
```
sudo apt update; sudo apt upgrade
```
![image](https://user-images.githubusercontent.com/36489276/202257184-d1a17a14-5a56-4692-b012-e38938e3156c.png)
bila ada output untuk meminta konfirmasi itu, kita tinggal ketik y saja

selanjutanya kita perlu mengguanakan pip, pip merupakan package manager dari python3, fungsinya sama seperti npm
```
sudo apt install python3-pip
```
![image](https://user-images.githubusercontent.com/36489276/202258565-3e52f462-3d32-4486-b93d-c5473b3a7785.png)
jika muncul output konfirmasi lagi, kita ketik y lagi

setelah itu, kita perlu untuk mengunduh framework flask
```
pip install flask
```
![image](https://user-images.githubusercontent.com/36489276/202263470-4fbcb71a-d89c-476d-8da0-0960ef2a3c4a.png)

setelah itu kita buat file pythonnya, saya akan menggunakan nama sayMyName.py
```
nano sayMyNameFromPython.py
```
kita isikan sebagai berikut:
```
from flask import Flask
app = Flask(__name__)
@app.route("/")
def helloworld():
    return "Reiya Tenggara"
if __name__ == "__main__":
    app.run()
```
![image](https://user-images.githubusercontent.com/36489276/202548055-6572444a-0935-4352-b717-866a5a06515f.png)

untuk mendeploy secara lokal, kita menggunakan perintah:
```
python3 sayMyNameFromPython.py
```
![image](https://user-images.githubusercontent.com/36489276/202428071-64a036a0-70aa-4ed4-80d0-9c42d36dbba2.png)

setelah itu kita copykan ip dan portnya, lalu tes di browser kita, bila berhasil, maka akan muncul seperti ini:
![image](https://user-images.githubusercontent.com/36489276/202548158-2144d043-a08c-4b43-a404-532bbceebb88.png)


untuk mendeploy menggunakan pm2 dan di deploy ke localtunnel, kita ketikan perintah
```
pm2 start sayMyNameFromPython.py --interpreter python3
```
![image](https://user-images.githubusercontent.com/36489276/202269645-8df26ed3-daf6-48e2-98e6-cc7fe7262012.png)

lalu kita gunakan localtunnel di port 5000
```
lt --port 5000
```
![image](https://user-images.githubusercontent.com/36489276/202270162-d43990c9-086b-43eb-ba9f-99d591bd6b0f.png)
lalu kita copy pastekan linknya dan buka dari web browser
![image](https://user-images.githubusercontent.com/36489276/202270554-2fb4b07b-9e9d-40ae-ba44-6985075818f8.png)


# 4. Deploy npm dengan localtunnel menggunakan pm2
setelah itu, kita akan mendeploy dengan menggunakan localtunnel, bila localtunnel belum terinstal, kita bisa menginstallnya dengan mengetikan perintah:
```
npm install -g localtunnel
```
![image](https://user-images.githubusercontent.com/36489276/202157799-b7ac4eeb-c1e0-456c-8dee-fb7cb59030a7.png)

lalu kita jalankan pm2 menggunakan perintah
```
pm2 start 'npm start'
```
![image](https://user-images.githubusercontent.com/36489276/202506776-50ce52b1-37a0-497b-b5cb-b1cd1b597fd7.png)


setelah itu, jalankan localtunnel di port 3000
```
lt --port 3000
```
![image](https://user-images.githubusercontent.com/36489276/202219822-c3459973-7e93-4e0f-837b-e2381007c563.png)

langkah terakhir, untuk mengecek apakah sudah terdeploy dengan benar, kita copy kan urlnya, lalu paste di web browser
![image](https://user-images.githubusercontent.com/36489276/202220727-25f55152-d811-425b-a478-49f0c6638a44.png)



Kita harus menginstall engine node js terlebih dahulu dengan menggunakan perintah:
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
![image](https://user-images.githubusercontent.com/36489276/202117375-f4be4e28-9308-4036-b371-5cc3a06624b1.png)

lalu ketikan perintah exec bash untuk melakukan soft restart ubuntu:
```
exec bash
```
![image](https://user-images.githubusercontent.com/36489276/202118095-30d7988a-f299-4689-ab1c-2853e1d6d153.png)

kita install nvm 16 dengan menggunakan perintah:
```
nvm install 16
```
![image](https://user-images.githubusercontent.com/36489276/202118541-fe4fdef8-c4a5-488e-98a5-d31c89395ffd.png)


Secara default kita seharusnya langsung menggunakan nvm 16, tapi jika anda berada dalam nvm versi lain dan ingin berpindah menggunakan nvm versi 16
jika ingin menggunakan nvm 16 kita dapat menggunakan perintah:
```
nvm use 16
```
![image](https://user-images.githubusercontent.com/36489276/202118929-a63cc88f-07dc-4fd4-be33-933a0ea797ac.png)

untuk mengecek versi node js dan node package manager, kita bisa menggunakan perintah:
```
node -v #untuk mengejek versi node js
```
```
npm -v #untuk mengecek versi node package manager
```

Pada kasus kali ini, karena kita akan mendeploy aplikasi yang sudah ada di dalam repository github, kita perlu melakukan proses cloning terlebih dahulu menggunakan perintah
```
git clone  https://github.com/dumbwaysdev/wayshub-frontend
```
Ganti link tersebut sesuai dengan kebutuhan anda

setelah proses cloning berhasil, 

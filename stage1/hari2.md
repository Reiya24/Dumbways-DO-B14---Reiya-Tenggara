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



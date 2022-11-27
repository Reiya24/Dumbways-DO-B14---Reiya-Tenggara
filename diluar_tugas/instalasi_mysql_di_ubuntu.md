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

catatan : kita tidak bisa langsung menggunakan command mysql_secure_installation, Karena akan terjadi recrusive loop pada saat
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
- Permintaan Password Mysql sangat ketat, jika anda ingin menggunakan password mysql dengan singkat, jangan lupa konfigurasi terlebih dahulu
```
SET GLOBAL validate_password.LENGTH = 4;
SET GLOBAL validate_password.policy = 0;
SET GLOBAL validate_password.mixed_case_count = 0;
SET GLOBAL validate_password.number_count = 0;
SET GLOBAL validate_password.special_char_count = 0;
SET GLOBAL validate_password.check_user_name = 0;
ALTER USER 'user'@'localhost' IDENTIFIED BY 'pass';
FLUSH PRIVILEGES;
```
setelah itu, saya dapat membuat passwordnya lebih singkat
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '1234';
```
![image](https://user-images.githubusercontent.com/36489276/204157654-ad5dff3a-0b09-4da5-a611-dd9ba00045f8.png)





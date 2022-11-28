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
setelah itu exit
```
exit
```
![image](https://user-images.githubusercontent.com/36489276/204352169-f1cd65f2-730c-417c-9f9b-773540f7612d.png)






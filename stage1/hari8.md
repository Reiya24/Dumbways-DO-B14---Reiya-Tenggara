# 1 definisi web server

# 2. Jalankan 2 VM

pada kasus ini saya akan menginstall 2 virtual machine dengan menggunakan multipass.
cara membuatnya cukup gunakan perintah

```
multipass launch 20.04 --name multipass1
```

artinya saya akan menginstall sebuah virtual machine berbasis ubuntu 20.04 dengan nama multipass1

karena saya akan menginstall 2 virtual machine, saya akan mengulangi perintah yang sama dengan nama virtual machine yang berbeda

```
multipass launch 20.04 --name multipass2
```

untuk menjalankannya, ketikan perintah
```
multipass shell nama_vitual_machine
```
![image](https://user-images.githubusercontent.com/36489276/203630079-fbe4ecd2-b05a-4e99-ae7b-a36b58d1296e.png)

virtual machine pertama akan digunakan untuk appserver nginx, kita perlu menginstallnya terlebih dahulu dengan menggunakan perintah
```
sudo apt install nginx
```
![image](https://user-images.githubusercontent.com/36489276/203630536-698bbc13-6c23-4123-9c69-516040b35b93.png)

kita cek apakah sudah terinstall dengan benar, kita bisa mengeceknya dengan mengecek versi nginx itu sendiri, gunakan perintha
```
nginx -v
```
![image](https://user-images.githubusercontent.com/36489276/203630943-dcf3f30d-2275-48a1-be8b-796407c50cc1.png)


setelah itu, kita hidupkan service nginx dengan menggunakan perintah
```
sudo systemctl enable nginx
```
![image](https://user-images.githubusercontent.com/36489276/203632081-cda75c9d-b0a2-45fa-8713-963d0313f884.png)

lalu kita jalankan service nginx dengan menggunakan perintah 
```
sudo systemctl start nginx
```
![image](https://user-images.githubusercontent.com/36489276/203632254-3ca29c0a-4d46-4414-a5d6-710c4551593d.png)


setelah itu, check apakah service nginx sudah berjalan di background, gunakan perintah
```
sudo systemctl status nginx
```
![image](https://user-images.githubusercontent.com/36489276/203631393-172a7356-7be3-41fc-9769-3cdde85dd138.png)
bila status Active: sudah active (berwarna hijau) maka service nginx sudah aktif

lalu, cek apakah nginx sudah dapat berjalan di pc utama kita, denga memasukan IP dari multipass tersebut, untuk mengeceknya, gunakan perintah:
```
hostname -I
```
![image](https://user-images.githubusercontent.com/36489276/203633763-72a07070-ad81-4c62-a68a-fff12267f0ca.png)

![image](https://user-images.githubusercontent.com/36489276/203634001-0229f0c0-0da4-480d-ab2f-1ae9733bfcf2.png)

jika muncul seperti ini, artinya service nginx berhasil dijalankan

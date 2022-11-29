pada kasus kali ini, saya memiliki ubuntu server yang berada di cloud

## 1. menggunakan ssh

pada komputer utama kita, ketikan
```
ssh username@ip_public
```
![image](https://user-images.githubusercontent.com/36489276/204488467-10e685dc-de49-45ae-a4fa-5e2302cfb315.png)
username saya adalah reiya_singapur dan ip publik saya adalah 103.13.206.167
maka masukan
```
ssh reiya_singapur@103.13.206.167
```
jika muncul konfirmasi, ketik yes.
lalu masukan password ubuntu server

sumber : https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server-id

## 2. menggunakan ssh keygen

buat kunci ssh, (biasanya di komputer kita) menggunakan :
```
ssh-keygen
```

lalu, masukan lokasi kunci yang akan di generate, saya akan memasukannya ke dalam folder .my_config
```
/home/nama_user_folder/.nama_folder_ssh/nama_file_ssh
```
![image](https://user-images.githubusercontent.com/36489276/204497266-d5c7e3fc-f403-4334-82c5-811ac5480d45.png)

masukan passphrase, (bisa di skip, tekan enter saja untuk melanjutkan)

setelah di generate, kita copy isi dari nama file ssh .pub tadi untuk dimasukan ke vm ubuntu server
```
cat nama_file_ssh.pub
```
![image](https://user-images.githubusercontent.com/36489276/204526449-e4042e6e-1232-4948-9cf4-a22b606b8011.png)

Setelah itu kita masuk ke ubuntu server kita,
lalu paste file tadi ke .ssh/authorized_keys
```
nano .ssh/authorized_keys
```
![image](https://user-images.githubusercontent.com/36489276/204527099-207b6db4-79d3-4a4f-b58d-ac2e139f28de.png)

lalu paste isi pub tadi
![image](https://user-images.githubusercontent.com/36489276/204527327-d1beea00-6d1d-4882-a120-cd7daaac9adb.png)

Setelah itu kita akan mencoba login menggunakan ssh di komputer utama kita

```
ssh -i nama_file_ssh reiya_singapur@103.13.206.167
```
![image](https://user-images.githubusercontent.com/36489276/204528210-3fff134d-51cf-41e8-af27-7fd82a3eb320.png)


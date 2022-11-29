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
/home/nama_user_folder/.nama_folder_ssh/nama_file_Ssh
```
![image](https://user-images.githubusercontent.com/36489276/204497266-d5c7e3fc-f403-4334-82c5-811ac5480d45.png)

masukan passphrase, (bisa di skip, tekan enter saja untuk melanjutkan)



sumber https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-20-04

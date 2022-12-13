saya membuat sebuah script untuk installer ansible
```
#!/bin/bash
sudo apt install -y software-properties-common #instal depedensi yang diperlukan
sudo add-apt-repository --yes --update ppa:ansible/ansible #tambahkan repository untuk ansible
sudo apt update #lakukan update
sudo apt install -y ansible #install ansible
ansible --version #cek versi dari ansible
```
![image](https://user-images.githubusercontent.com/36489276/207254765-68c3de55-73ec-40f8-ba58-e0b78038be41.png)

ubah perizinan scriptnya
```
chmod 700 ansible_installer.sh
```

![image](https://user-images.githubusercontent.com/36489276/207254824-e79b552a-136f-4706-b625-ff7bd3ef2c32.png)

jalankan scriptnya
![image](https://user-images.githubusercontent.com/36489276/207255574-a16c2e04-aa28-4485-8d47-3b3ff8d0c7a4.png)

# setup SSH keyless
saya akan buat sebuah ssh dengan nama dan direktori default
![image](https://user-images.githubusercontent.com/36489276/207267225-d8a029e8-b20b-4c62-85a2-d22578bb8bcf.png)

lalu copy publik key ke server tujan kita menggunakan ssh-copy-id
```
ssh-copy-id -f -i ~/.ssh/id_rsa.pub  appserver@103.187.147.8
```
![image](https://user-images.githubusercontent.com/36489276/207267682-c510de0a-41ac-48c6-a30a-6cc24013a126.png)
ketik yes, lalu masukan password

jika berhasil kita bisa masuk ke server tersebut tanpa menggunakan password
![image](https://user-images.githubusercontent.com/36489276/207267950-c39f1931-e357-43ba-9a4f-06266f4cf7fe.png)

# buat file intentori
buat file inventori yang berfungsi untuk menyimpan informasi server2 yang akan kita konfigurasi, disini saya akan memasukan appserver dan gateway
![image](https://user-images.githubusercontent.com/36489276/207269044-d459886e-f68b-4135-9243-c1a5639eac10.png)

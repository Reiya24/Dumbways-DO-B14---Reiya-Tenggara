# 1 definisi web server

# 2. Jalankan 2 VM

pada kasus ini saya akan menginstall 2 virtual machine dengan menggunakan multipass.
cara membuatnya cukup gunakan perintah

```
multipass launch 20.04 --name multipass1
```
![image](https://user-images.githubusercontent.com/36489276/203636495-94623a0b-3612-4f57-8267-7e9cb4331574.png)


artinya saya akan menginstall sebuah virtual machine berbasis ubuntu 20.04 dengan nama multipass1

karena saya akan menginstall 2 virtual machine, saya akan mengulangi perintah yang sama dengan nama virtual machine yang berbeda

```
multipass launch 20.04 --name multipass2
```
![image](https://user-images.githubusercontent.com/36489276/203636650-02bf7997-5081-4c32-9941-9c6e1a217573.png)


untuk menjalankannya, ketikan perintah
```
multipass shell nama_vitual_machine
```
![image](https://user-images.githubusercontent.com/36489276/203630079-fbe4ecd2-b05a-4e99-ae7b-a36b58d1296e.png)

virtual machine pertama akan digunakan untuk appserver dumflix-frontend, sebelum menjalankannya kita perlu menginstall node js terlebih dahulu.
kita akan gunakan script installer yang sudah dibuat untuk mempercepat proses deployment
```
nano node_js_installer.sh
```
![image](https://user-images.githubusercontent.com/36489276/203637589-d95384f4-ceef-4b13-a5a1-02c1a4754a78.png)


isikan
```
#!/bin/bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
eval "$(cat ~/.bashrc | tail -n +10)"
nvm install 16
nvm use 16
node -v
npm install pm2 -g
exec bash
```
![image](https://user-images.githubusercontent.com/36489276/203638399-647cf500-f5bd-4cce-ae5a-da355b56a654.png)

setelah itu berikan permission untuk execute
```
chmod +x node_js_installer.sh
```
![image](https://user-images.githubusercontent.com/36489276/203637659-32ddde4b-2efa-4efc-bc40-87b76dff6eaf.png)

lalu jalankan scriptnya
```
./node_js_installer.sh
```
![image](https://user-images.githubusercontent.com/36489276/203638590-8685f6d4-cefc-44ef-bd10-bd9a03ac52a2.png)

setelah itu, lakukan cloning project dumbflix-frontend
```
git clone https://github.com/dumbwaysdev/dumbflix-frontend
```
![image](https://user-images.githubusercontent.com/36489276/203639637-997e5168-a1d0-41b0-a84a-e85303cdfa75.png)

setelah itu masuk ke direktori dumbflix, lalu lakukan npm install untuk menginstall depedensi yang dilakukan
```
npm install
```
![image](https://user-images.githubusercontent.com/36489276/203640921-97e6d661-d5c7-4878-af88-d96200fd2e24.png)

lalu jalankan melalui pm2
```
pm2 start npm --name "dumbflix_frontend" -- start
```
![image](https://user-images.githubusercontent.com/36489276/203641179-1cd0ffd4-6558-46af-9948-2989f0d2bd99.png)

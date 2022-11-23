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

# 3 VM 1, digunakan untuk menjalankan dumbflix-fronted menggunakan PM2

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

jangan lupa untuk setting firewall agar aplikasi dapat diakses di pc utama pada port 3000
```
sudo ufw enable
sudo ufw allow 3000
```
![image](https://user-images.githubusercontent.com/36489276/203641981-fa6cbcbb-3f7c-454a-b600-e6ea4e885d83.png)

lalu coba akses di pc utama kita dengan memasukan alamat di browser
```
ip:3000
```
untuk melihat ip, kita dapat menggunakan perintah
```
hostname -I
```
![image](https://user-images.githubusercontent.com/36489276/203642394-79e50ba4-0444-4949-9197-0b34187c144b.png)

jika muncul homepage dumbflix, maka proses menjalankan appserver dumbflix-frontend telah selesai

# 4 jalankan vm 2 untuk menjalankan nginx

lakukan proses instalasi nginx terlebih dahulu
```
sudo apt install nginx
```
![image](https://user-images.githubusercontent.com/36489276/203644462-30a0e8ee-722a-46d2-b430-12f506eda3be.png)

setelah itu, kita menyalakan service nginx, kita dapat gunakan perintah
```
sudo systemctl enable nginx
```
![image](https://user-images.githubusercontent.com/36489276/203644786-2949c00f-442b-4862-b08a-6c7865ade5b3.png)

untuk menjalankan prosesnya, gunakan:
```
sudo systemctl start nginx
```
![image](https://user-images.githubusercontent.com/36489276/203644845-5bc56f70-8990-43df-90d1-6a30a77e4730.png)

lalu cek service nginx untuk memastikan apakah sudah aktif, gunakan perintah
```
sudo systemctl status nginx
```
![image](https://user-images.githubusercontent.com/36489276/203645299-fc8b016e-c947-497a-9911-a69d4a5b9f6c.png)

lalu kita masukan IP multipass tadi ke pc utama kita untuk mengecek apakah sudah berjalan
![image](https://user-images.githubusercontent.com/36489276/203648712-62b53a33-fc5c-40ab-81a4-9f10a58cc56b.png)

setelah itu, kita akan mengkonfigurasi reverse proxy

masuk ke direktori konfigurasi nginx, yaitu di cd /etc/nginx
```
cd /etc/nginx
```

lalu buat folder konfigurasi, saya akan membuat folder dengan nama saya
```
sudo mkdir reiyatenggara
```
lalu masuk  ke folder tersebut
```
cd reiyatenggara
```

setelah itu, buat file konfigurasinya
```
sudo nano my.reverse-proxy.conf
```

masukan
```
server {
    server_name reiyatenggara.xyz;

    location / {
             proxy_pass http://172.30.63.239:3000;
    }
}
```
![image](https://user-images.githubusercontent.com/36489276/203650025-26e34cfb-cddb-4702-90b7-d4594ae95f59.png)

sesuaikan server_name dengan nama domain yang ingin anda pakai
lalu sesuaikan proxy_pass dengan IP pada virtual machine pertama

setelah di save pergi ke direktori sebelumnya
```
cd ..
```

setelah itu kita perlu mengatur konfigurasi dari file ngix.conf
```
sudo nano nginx.conf
```
![image](https://user-images.githubusercontent.com/36489276/203650850-558c9518-c141-42a8-86f1-88521328d951.png)

lalu cari ke bagian include,
setelah itu tambahkan file konfigurasi file kita
```
include /etc/nginx/reiyatenggara/*;
```
![image](https://user-images.githubusercontent.com/36489276/203650587-fb2178e3-92ab-4988-a6f4-25291bdf60ee.png)

setelah di save, kita lakukan pengecekan syntax untuk memastikan apakah ada kesalahan dalam penulisan kode
```
sudo nginx -t
```
![image](https://user-images.githubusercontent.com/36489276/203651036-ad9b12f3-7a57-49b7-b44c-82d0309cbd69.png)
jika muncul seperti diatas, berarti tidak ada syntax error

setelah itu, kita perlu melakukan reload nginx kita akar nginx dapat mengenali perubahan file konfigurasi kita
```
sudo systemctl reload nginx
```
![image](https://user-images.githubusercontent.com/36489276/203651273-dbff9d75-fcdd-4cc4-adf8-ddcc21bd4aa0.png)

setelah itu kita perlu setting host file yang ada di pc utama kita
karena saya menggunakan windows, host filenya berada di
```
c:\Windows\System32\Drivers\etc\hosts
```

masukan IP dari virtual machine nginx, serta nama domain yang akan kita gunakan
![image](https://user-images.githubusercontent.com/36489276/203651931-f2feb399-a884-4529-84ea-f105f732872a.png)



# Install Docker menggunakan bash script

buat file bash script untuk installer docker
```
read -p "ketik y untuk menginstall docker, ketik sembarang kata untuk membatalkan   " choice

if [ $choice = "y" ]
then
    echo "###########################"
    echo "update repository"
    echo "###########################"
    sudo apt-get update -y

    echo "menghapus semua versi lama docker bila ada"
    sudo apt-get remove docker docker-engine docker.io containerd runc -y
    
    echo "###########################"
    echo "install depedency yang diperlukan"
    echo "###########################"
    sudo apt-get install \
        ca-certificates \
        curl \
        gnupg \
        lsb-release
    
    echo "###########################"
    echo "install GPG key"
    echo "###########################"
    sudo mkdir -p /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

    echo "###########################"
    echo "set up repository"
    echo "###########################"
    echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    echo "###########################"
    echo "update repository lagi"
    echo "###########################"
    sudo apt-get update -y
    
    echo "###########################"
    echo "install docker engine, containerd, dan docker compose"
    echo "###########################"
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y

    echo "###########################"
    echo "tambahkan user yang ada sekarang ke dalam grup docker"
    echo "###########################"
    sudo usermod -aG docker $(whoami)
    pwd
    
    echo "###########################"
    echo "docker berhasil di install"
    echo "###########################"
    exec bash
else
    echo "script berhenti"
fi
```
![image](https://user-images.githubusercontent.com/36489276/205584510-b595295b-8976-4f5d-b23d-00f60e35fa76.png)

setelah itu jalankan perintah chmod untuk memberi akses kepada user untuk melakukan read, write dan execute
```
chmod 700 docker_installer.sh
```

jalankan docker installer
```
./docker_installer.sh
```
![image](https://user-images.githubusercontent.com/36489276/205585816-746569b7-e55b-46b6-b029-64f0a54f473f.png)
ketik y untuk melanjutkan

![image](https://user-images.githubusercontent.com/36489276/205587672-4213c0fb-c03e-4e50-a362-fdf1d5a31f5a.png)

# install node js dan sequelize-cli
buat file untuk node js installer
```
nano node_js_installer.sh
```
isikan script berikut
```
#!/bin/bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
eval "$(cat ~/.bashrc | tail -n +10)"
nvm install 10
nvm use 10
node -v
npm install pm2 -g
npm install -g sequelize-cli
exec bash
```
![image](https://user-images.githubusercontent.com/36489276/205590861-0417264f-638e-4186-a9fe-c8acc08d029f.png)

setelah di save, tambahkan perizinan agar bisa dieksekusi
```
chmod 700 node_js_installer.sh
```
![image](https://user-images.githubusercontent.com/36489276/205591097-91e47e8b-e460-4599-b9a4-1115ec03e850.png)

eksekusi filenya
```
./node_js_installer.sh
```
![image](https://user-images.githubusercontent.com/36489276/205591984-d1bdf9e3-a574-4311-bcfe-43482092f8eb.png)

# daftarkan domain di cloudflare
buka dashboard clouflare https://dash.cloudflare.com/ . setelah itu pilih akun

klik student dumbwyas
![image](https://user-images.githubusercontent.com/36489276/205646763-9748d71b-efa4-4261-99c8-e8e4bcd98ecc.png)

pilih dns
![image](https://user-images.githubusercontent.com/36489276/205646828-7edb5892-f206-44f3-9b50-e993f29377e0.png)

klik add record, llu masukan nama domain, lalu masukan IP public gateway, matikan proxy status, lalu save. Untuk backend, lakukan proses yang sama
namun ditambah api.
![image](https://user-images.githubusercontent.com/36489276/205647075-1d7a40cd-d831-48f8-9ca2-3bb380db3cac.png)

# Setup Housy-Frontend
Clone terlebih dahulu project housy-frontend
```
git clone https://github.com/dumbwaysdev/housy-frontend
```
![image](https://user-images.githubusercontent.com/36489276/205594850-72f5d9de-563d-4053-8a70-f4ae210fad42.png)

masuk ke direktori tersebut

kita perlu untuk mengkonfigurasi frontend agar dapat berkomunikasi dengan backend, edit file /src/config/api.js.
ubah alamat baseURL menjadi alamat domain backend kita
```
nano src/config/api.js
```
![image](https://user-images.githubusercontent.com/36489276/205678772-41886777-e843-4de6-9f11-dd4c691f0234.png)


buat sebuah dockerfile untuk kita build menjadi docker image
```
nano Dockerfile
```

setelah itu isikan sebagi berikut
```
FROM node:10.24.0-alpine3.10
WORKDIR ./app
COPY . .
RUN npm install
EXPOSE 3001
CMD ["npm","start"]
```
![image](https://user-images.githubusercontent.com/36489276/205603385-4781f6b2-63ef-4c09-85d2-34fcc09f1631.png)

setelah itu, build docker image dengan menggunakan perintah
```
docker build -t reiya/housy-frontend .
```
![image](https://user-images.githubusercontent.com/36489276/205602775-d38a79eb-3303-4394-bd16-bdddb46d0c30.png)

jika sudah, liat hasil image yang di build menggunakan perintah
```
docker image ls
```
![image](https://user-images.githubusercontent.com/36489276/205616621-491cd7d6-1b12-4d37-bc7c-1109d7200f8c.png)

lalu kita akan membuat sebuah file yang bernama docker-compose.yml, yang berisikan perintah untuk membuild sebuah container dari sebuah image yang sudah kita buat
```
version: '3.8'
services:
 frontend:
   container_name: frontend
   image: reiya/housy-frontend
   stdin_open: true
   ports:
    - 3001:3000
```
![image](https://user-images.githubusercontent.com/36489276/205677572-1f848a00-4c5a-4552-8bc1-4fb408e1fdb0.png)

jalankan docker compose
```
docker compose up -d
```
![image](https://user-images.githubusercontent.com/36489276/205678052-6f8e23ea-8e45-41bd-b7cf-63db10473864.png)

docker container sudah berjalan
![image](https://user-images.githubusercontent.com/36489276/205680223-68102885-fa4b-4ae8-b13a-10eb730d4b7e.png)

# Setup housy backend
clone terlebih dahulu housy backend, setelah itu masuk ke dalam direktori tersebut

konfigurasi file database yang berada di config/config.json, sesuaikaun username, password dan nama database
```
nano config/config.json
```
![image](https://user-images.githubusercontent.com/36489276/205682015-9d19e780-9159-4a5f-aea1-f78ad32aebd2.png)

setelah itu, kita akan membuat sebuah Dockerfile untuk membuat sebuah image yang ingin kita buat, masukan :
```
FROM node:15

ENV NODE_ENV development

WORKDIR /home/root
COPY . .

RUN npm install
RUN npx sequelize db:migrate --env development
EXPOSE 5000
CMD ["npm","start"]
```
![image](https://user-images.githubusercontent.com/36489276/205682403-11902ffb-60bb-4822-a2ce-0db47553192b.png)

setelah itu, build dockerfilenya dengan menggunakan perintah:
```
sudo docker build -t angga/housy-backend .
```
![image](https://user-images.githubusercontent.com/36489276/205683064-c2d76e11-1943-4076-91cc-417461720fa5.png)

lalu, setelah itu jalankan docker compose untuk membuat container housy backend
![image](https://user-images.githubusercontent.com/36489276/205683328-f3b06697-f3e0-4573-b1ff-7134d3c849c8.png)

# setup database mysql
buat sebuah file bernama mysql.yml yang berisikan script docker compose untuk membuild sebuah container dari image mysql
```
version: '3.8'

services:
  db:
    image: mysql:8
    environment:
      MYSQL_DATABASE: 'housy'
      MYSQL_USER: 'angga'
      MYSQL_PASSWORD: 'P4ssw0rd'
      MYSQL_ROOT_PASSWORD: 'P4ssw0rd'
    ports:
      - '3306:3306'
    expose:
      - '3306'
    volumes:
      - /tmp/mysql-data:/var/lib/mysql\
```
![image](https://user-images.githubusercontent.com/36489276/205684066-4a5741da-60eb-4293-8b8b-5cf1b080efdd.png)

setelah itu jalankan docker compose menggunakan perintah
```
docker compose -f mysql.yml up -d
```
![image](https://user-images.githubusercontent.com/36489276/205684308-a82776a8-84f1-4118-a3d5-c0cb8d196c56.png)


# instalasi nginx pada webserver
lakukan update package
```
sudo apt update -y
```
![image](https://user-images.githubusercontent.com/36489276/205620053-807b1fa2-2641-477b-86dc-e95cf770dab2.png)

install nginx
```
sudo apt install nginx -y
```
![image](https://user-images.githubusercontent.com/36489276/205620259-15f2e542-d922-49d7-a498-d06f9e33db6a.png)

setelah itu, buat folder baru untuk reverse proxy
```
sudo mkdir housy
```
![image](https://user-images.githubusercontent.com/36489276/205620473-0fed2506-bac8-4f9d-98dc-4742be141f38.png)

untuk membuat direktori housy terbaca oleh nginx, kita perlu mengaturnya di file nginx.conf
```
sudo nano nginx.conf
```

hapus tanda pagar yang pada baris yang ditandai agar kita dapat menggunakan domain yang panjang
![image](https://user-images.githubusercontent.com/36489276/205621089-66739d43-348b-4a85-8be1-b8cab96711a8.png)


setelah itu, pergi ke baris bawah sampai menemukan kata include.
tambahkan lokasi direktori housy agar nginx mau membacanya
```
include /etc/nginx/housy/*;
```
![image](https://user-images.githubusercontent.com/36489276/205621240-6e79c928-f056-468e-87de-6d6067fbfbb1.png)

cek syntaxnya dengan menggunakan perintah
```
sudo nginx -t
```
![image](https://user-images.githubusercontent.com/36489276/205621719-e108e1f1-9bde-4ffc-a750-c5fd5148ff32.png)

setelah itu, buat konfigurasi reverse proxy, untuk frontend dan untuk backend

![image](https://user-images.githubusercontent.com/36489276/205634868-e1d5970f-b9dd-499e-a1f1-2cc843ad668d.png)
![image](https://user-images.githubusercontent.com/36489276/205634954-74657371-8698-43f5-9928-7d1aa54479ad.png)


# Instalasi Certbot untuk Https

lakukan proses update pada snap agar mendapatkan versi terbaru dari snapd
```
sudo snap install core; sudo snap refresh core
```
![image](https://user-images.githubusercontent.com/36489276/205630257-c9ec91a4-91c1-444a-8ef2-841f7840b76a.png)


setelah itu install certbot menggunakan snap
```
sudo snap install --classic certbot
```
![image](https://user-images.githubusercontent.com/36489276/205629776-bbaad16b-657e-42d5-89d2-91128e8f0b3b.png)

tambahkan path certbot agar perintah certbot dapat dijalankan
```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
![image](https://user-images.githubusercontent.com/36489276/205630486-2b999fa8-0deb-49da-bee2-23f350a3adab.png)

jalankan certbot
```
sudo certbot --nginx
```
![image](https://user-images.githubusercontent.com/36489276/205630913-1f830451-302f-4046-89c7-62fc9cf1b7ab.png)

masukan email untuk mendapatkan pemberitahuan dari certbot
![image](https://user-images.githubusercontent.com/36489276/205630985-46d153cb-ac68-43d5-8c2f-17bc5186f3ad.png)

alu kita harus setuju dengan syarat dan ketentuan, pilih y 
![image](https://user-images.githubusercontent.com/36489276/205631060-96606a48-3684-4113-bd7d-1d55020a698f.png)

pilih n agar tidak langganan email ke Electronic frontier foundation 
![image](https://user-images.githubusercontent.com/36489276/205631180-666bbf96-97c4-4e02-b12c-42c94e359f67.png)

pilih enter untuk pilih semua domain
![image](https://user-images.githubusercontent.com/36489276/205631465-17f33ce6-6298-4c65-838f-bc4b8453835e.png)

pemasangan berhasil
![image](https://user-images.githubusercontent.com/36489276/205631583-4ac30909-c0d5-4b45-954a-3aaa47f94b86.png)

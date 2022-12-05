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


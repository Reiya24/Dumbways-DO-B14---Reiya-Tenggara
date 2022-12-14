# Jalankan Jenkins on top docker

Install docker terlebih dahulu,
setelah itu, kita akan menginstall jenkins menggunakan docker compose
buat docker compose terlebih dahulu
```
nano docker-compose.yaml
```

isikan kurang lebih sebagai berikut
```
version: '3.7'
services:
  jenkins:
    container_name: jenkins
    image: jenkins/jenkins:latest-jdk11
    privileged: true
    user: root
    restart: unless-stopped
    ports:
      - 8123:8080
    volumes:
      - ~/jenkins_config:/var/jenkins_home
      - ~/jenkins-docker-certs:/certs/client
```
![image](https://user-images.githubusercontent.com/36489276/206370212-c8f35167-2e4b-4c2b-9c89-0547c1e80e67.png)


jalankan docker compose
```
docker compose up -d
```
![image](https://user-images.githubusercontent.com/36489276/206370178-bb7db07b-9434-4a8f-8e78-2859b7fd9ebe.png)

setelah itu, kita perlu melihat password untuk melakukan setup jenkins, gunakan perintah container logs untuk melihat password
```
docker container logs jenkins
```
![image](https://user-images.githubusercontent.com/36489276/206370739-39724abc-1966-4a9c-8ee4-ddf56adb7d7c.png)

untuk melakukan konfigurasi pada jenkins, kita dapat mengaksesnya dengan menggunakan ip publik virtual machine kita, dan tambahkan port yang sudah kita setel

masukan password yang ada di logs tadi, kemudian klik continue
![image](https://user-images.githubusercontent.com/36489276/206373033-30ab4d0b-7357-4a93-bc20-dfb0b4015e78.png)

setelah itu, klik select plugins to install, karena kita akan menambahkakn 1 plugin bernama ssh agent

cari ssh agent, ceklis, lalu klik install
![image](https://user-images.githubusercontent.com/36489276/206373320-aa749652-f6c6-42b9-bd7b-ace2547c58d5.png)

tunggu sampai proses instalasi berhasil
![image](https://user-images.githubusercontent.com/36489276/206373778-0d5ef854-5acc-40ff-9484-27e165cf9dac.png)

setelah itu setup username, password, fullname, dan email
![image](https://user-images.githubusercontent.com/36489276/206375502-18f045ec-a933-453d-9992-8e9e79a797a6.png)

kita akan setup reverse proxy nanti, jadi pilih save and finish
![image](https://user-images.githubusercontent.com/36489276/206376858-f5835a27-25da-422c-87e9-067b8a9aee12.png)

pilih, start using jenkins
![image](https://user-images.githubusercontent.com/36489276/206376902-2b55a2ba-d9ab-4428-8b92-033b833f0a55.png)

# Setup SSH untuk jenkins dan github

kita perlu setup ssh terlebih dahulu di virtual machine kita
```
ssh-keygen
```
![image](https://user-images.githubusercontent.com/36489276/206378634-655b8182-8bee-4688-a36d-41b8182bbb9c.png)
sesuaikan direktori ssh yang ingin disimpan, dan sesuaikan passphrase yang diinginkan, saya akan membiarkan default

## Setup unuk github
pada tambhilan home github, klik logo profile kita lalu klik settings

![image](https://user-images.githubusercontent.com/36489276/206379166-6aa0c1b2-92b2-4a79-9949-4b4912ec9237.png)

pilih SSH dan GPG keys
![image](https://user-images.githubusercontent.com/36489276/206379275-0acb8afe-f83b-4e55-8710-2428e2c76091.png)

lalu klik new SSH keys
![image](https://user-images.githubusercontent.com/36489276/206379544-f13f0aa3-bcf8-422f-9f5d-df0a780317e1.png)

title sesuaikan dengan keinginan,
untuk key masukan public key dari ssh yang sudah kita generate di virtual machine kita lalu klik add keys
![image](https://user-images.githubusercontent.com/36489276/206380320-a35639c5-0137-41fe-8eb2-0a238b4c536d.png)

```
cat lokasi_file_gembok_ssh.pub
```
![image](https://user-images.githubusercontent.com/36489276/206379980-81ab867f-1f15-46e2-835a-04739ea48269.png)

SSH keys sudah ditambahkan
![image](https://user-images.githubusercontent.com/36489276/206380683-21edde7f-2b0b-4909-adf5-4a7938351d53.png)

## setup ssh untuk jenkins

pilih manage jenkins
![image](https://user-images.githubusercontent.com/36489276/206382002-069afbde-230c-419f-9dac-f732a78ae61b.png)

lalu pilih manage credentials
![image](https://user-images.githubusercontent.com/36489276/206382123-223f10e3-4142-40e1-9a86-1e7d6e0efa81.png)

klik system
![image](https://user-images.githubusercontent.com/36489276/206382682-d5251e35-b4a5-446d-bbaf-e6d7f304ec12.png)

klik global credentials (unrestricted)
![image](https://user-images.githubusercontent.com/36489276/206382814-1cb7c6a1-cbe5-4b5c-a28c-cea28413c66d.png)

pilih add credentials
![image](https://user-images.githubusercontent.com/36489276/206382859-2cb90a2f-c06a-47d2-8536-86eac7c26faf.png)

untuk kind, pilih ssh username with private keys, id dan description dan name gunakan sesuai kebutuhan
![image](https://user-images.githubusercontent.com/36489276/206383615-9fe0fc59-cb44-450a-8060-b3899ce6be8a.png)

untuk private key, pilih enter directly dan masukan private key yang sudah kita generate
```
cat lokasi_kunci_ssh
```
![image](https://user-images.githubusercontent.com/36489276/206384167-be675843-45ce-405c-9341-86fdbd267564.png)

![image](https://user-images.githubusercontent.com/36489276/206383962-4ea6f124-447c-4f05-981f-942ff9d6d375.png)

ssh berhasil ditambahkan
![image](https://user-images.githubusercontent.com/36489276/206384432-4165d491-42c6-43ba-a224-6e50765ed481.png)

# Pipeline untuk Frontend dan Backend

## Push dari repository lokal ke repository private github

kita akan melakukan git push ke github dari direktori housy_frontend yang ada di virtual machine.

tambahkan konfigurasi username dan email kita sebelum melakukan proses push
```
git config --global user.email "email"
git config --global user.name "password"
```
![image](https://user-images.githubusercontent.com/36489276/206459836-7518d25b-b7b7-47dc-82b9-0edb98362dcd.png)

tambahkan git add . untuk memindahkan semua kode dari working directory ke staging area
```
git add . 
```
![image](https://user-images.githubusercontent.com/36489276/206459934-326b5270-aefc-4a56-85c9-625211d6882e.png)

lakukan perintah commit untuk memindahkan dari staging area ke repository
```
git commit -m "pesan"
```
![image](https://user-images.githubusercontent.com/36489276/206461066-0ed857da-7d77-4d74-8395-060a09422201.png)

gunakan git branch untuk membuat branch main
```
git branch -M main
```
![image](https://user-images.githubusercontent.com/36489276/206461370-36d65d8b-c5b5-4f63-9964-b0e77c4657dd.png)

lalu kita tambahkan remote agar repository git dan repository github saling terhubung
```
git remote add origin git@github.com:Reiya24/housy-frontend.git
```
![image](https://user-images.githubusercontent.com/36489276/206463191-b78f759f-93f4-4bd0-a66d-15ce66b79744.png)


## Setup jenkins pipeline
untuk membuat sebuah pipeline baru, klik create a job
![image](https://user-images.githubusercontent.com/36489276/206452340-5d06e03e-7f95-458f-af34-90612b2a0e8a.png)

masukan nama, dan pilih pipeline
![image](https://user-images.githubusercontent.com/36489276/206455553-f4e16549-e29c-4150-930a-8266e41e8eee.png)

pada build trigger, klik "GitHub hook trigger for GITScm polling"
![image](https://user-images.githubusercontent.com/36489276/206455852-14adbf53-695e-4642-8bfa-d3e199e18a83.png)

pada menu pipeline
untuk definition pilih pipeline script from SCM

![image](https://user-images.githubusercontent.com/36489276/206470299-6d1c8c19-21d1-45ce-8557-89ac38d76800.png)

masukan script path untuk jenkins
![image](https://user-images.githubusercontent.com/36489276/206470790-2fe3a22c-81cb-4627-b476-5ae0c3c0e723.png)




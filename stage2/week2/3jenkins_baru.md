# 1 jalankan jenkins on top docker

buat sebuah docker compose untuk jenkins
![image](https://user-images.githubusercontent.com/36489276/206844004-fff84955-aed2-4d80-90ed-e0b6bb684520.png)

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
![image](https://user-images.githubusercontent.com/36489276/206844037-9ed163e3-cc07-4cb7-8a29-e571ce44a076.png)

jalankan docker compose
```
docker compose -f nama_file up -d
```
![image](https://user-images.githubusercontent.com/36489276/206844134-245ccf2b-b7e3-4e86-9277-6dcc05324cca.png)

setelah itu, kita perlu melihat password untuk melakukan setup jenkins, gunakan perintah container logs untuk melihat password, lalu copy passwrod tersebut
```
docker continaer logs nama_container
```
![image](https://user-images.githubusercontent.com/36489276/206844546-acad9fe1-22b5-473b-a40a-8d7e5c48b8d3.png)

atau karena kita sudah melakukan proses mounting pada jenkins, kita bisa melihatnya menggunakan perintah cat, namun kita harus menggunakan akun superuser
```
cat jenkins_config/secrets/initialAdminPassword
```
![image](https://user-images.githubusercontent.com/36489276/206845102-5e1c7ca2-814b-4810-a902-f8893c765fbb.png)

masuk ke setup jenkins menggunakan ip publik yang kita masukan ditambah port yang sudah didefinisikan, lalu paste password yang sudah dicopy
![image](https://user-images.githubusercontent.com/36489276/206846077-83a48c6e-51a1-42b0-948e-5aee60c23f8b.png)

pilih select plugin to install karena kita akan memasang plugin bernama ssh agent
![image](https://user-images.githubusercontent.com/36489276/206846200-84be0a51-2280-4d5b-b396-ad2f658877de.png)

cari ssh agent dan klik install
![image](https://user-images.githubusercontent.com/36489276/206846267-439f1065-550a-4e5e-81c0-a4ad1cca6385.png)

tunggu proses instalasi berhasil
![image](https://user-images.githubusercontent.com/36489276/206846856-231f2d58-6557-4129-b83f-db5aa797abe8.png)

masukan nama, password, full name, dan email
![image](https://user-images.githubusercontent.com/36489276/206849106-a20c767e-ee3e-44f6-bd2e-145a08d0bb4a.png)


kita akan melakukan reverse proxy nanti klik save and finish
![image](https://user-images.githubusercontent.com/36489276/206848973-854f739d-7240-4cd3-9600-343466dff1e0.png)

pilih start using jenkins
![image](https://user-images.githubusercontent.com/36489276/206849010-3c8a56cb-70bd-4be9-a59d-df14902c05d2.png)

# setup ssh

kita perlu setup ssh terlebih dahulu di virtual machine kita.
sesuaikan direktori ssh yang ingin disimpan, dan sesuaikan passphrase yang diinginkan, saya akan membiarkan default
```
ssh keygen
```
![image](https://user-images.githubusercontent.com/36489276/206849136-47bea59d-2ff4-4578-89b1-2e668af8994f.png)

pada dashboard jenkins, pilih manage jenkins
![image](https://user-images.githubusercontent.com/36489276/206849191-de6a2f0b-30d3-438a-a80b-8c0e7e1ad188.png)

pilih manage credentials
![image](https://user-images.githubusercontent.com/36489276/206849209-e071b081-51f4-4b4c-8e18-b882d2683b3a.png)

pilih system
![image](https://user-images.githubusercontent.com/36489276/206849228-0cdf66df-b368-491b-ace7-f80a5c880542.png)

pilih global credentials (unrestricted)
![image](https://user-images.githubusercontent.com/36489276/206849241-a32a343e-c2e5-464f-92b2-23e35051bd9a.png)

pilih add credentials
![image](https://user-images.githubusercontent.com/36489276/206849370-b01f40f8-0dd6-4290-82db-6f682948c7b6.png)

untuk kind, pilih SSH username with private key, sesuaikan id, description dan username, untuk private key pilih add directly, masukan private key ssh kita
![image](https://user-images.githubusercontent.com/36489276/206849833-614ac4ba-5051-4f64-8be6-5e89c2b7cbd3.png)

untuk mencari dimana private key ssh kita, di virtual machine kita, gunakan cat untuk mengcopy privete key kita, masukan lokasi dimana kita menyimpan ssh
```

```
![image](https://user-images.githubusercontent.com/36489276/206850012-d95ff64d-a8e4-4486-bc70-55d13a00975d.png)

setup ssh untuk jenkins berhasil
![image](https://user-images.githubusercontent.com/36489276/206850041-ca7cf949-716e-4591-a1e0-f7b0d5785b47.png)

# setup ssh untuk github

buka halaman github
![image](https://user-images.githubusercontent.com/36489276/206850797-8bb44b38-ba32-475c-8ba9-caa980c5ed0a.png)

pilih icon profile kita dan pilih setting
![image](https://user-images.githubusercontent.com/36489276/206850823-5661d294-3d1d-453c-bbef-13143dab3526.png)

pilih SSH dan GPG keys
![image](https://user-images.githubusercontent.com/36489276/206850855-e188d91b-411d-4c68-94b7-f627e3b40d75.png)

pilih new SSH keys
![image](https://user-images.githubusercontent.com/36489276/206850872-05c9e261-acc2-49f9-9675-807ecc09f25b.png)

masukan title, dan public key kita
![image](https://user-images.githubusercontent.com/36489276/206850931-b573d261-f620-4697-aaaa-2a32ea53c029.png)

public key dapat dicari di virtual machine kita yang sudah kita setup
```
cat .ssh/id_rsa.pub
```

ssh keys berhasil ditambahkan
![image](https://user-images.githubusercontent.com/36489276/206851021-adaf54de-3898-46a3-8879-b299c9dff03e.png)





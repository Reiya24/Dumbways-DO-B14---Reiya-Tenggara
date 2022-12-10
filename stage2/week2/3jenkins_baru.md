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
![image](https://user-images.githubusercontent.com/36489276/206851021-adaf54de-3898-46a3-8879-b299c9dff03e.png)

ssh keys berhasil ditambahkan
![image](https://user-images.githubusercontent.com/36489276/206851316-8bfc9189-bfa8-4c3b-8c60-0696743d0288.png)

# setup authorized keys di virtual machine kita
agar jenkins dapat mengakses ssh kita, kita perlu setup authorized keys, gunakana ssh keys public di virtual machine kita, dan paste di authorized keys
![image](https://user-images.githubusercontent.com/36489276/206852231-e82c6e35-0528-4360-997f-9bb445374fff.png)

![image](https://user-images.githubusercontent.com/36489276/206852246-135afa14-340b-4a3c-aa3d-5ab542474d4c.png)

![image](https://user-images.githubusercontent.com/36489276/206852244-626a0796-7ce5-45da-a668-73317767c2cf.png)


# setup reverse proxy jenkins
buka dashboard cloudflare, pilih akun yang mempunyai domain
![image](https://user-images.githubusercontent.com/36489276/206851822-0366e715-1d51-4cc1-9df5-8297c5754dbe.png)

pilih domain yang tersedia
![image](https://user-images.githubusercontent.com/36489276/206851839-58a663c1-8c61-4662-9bd7-aad7badea47a.png)

pada menu sebelah kiri, pilih dns
![image](https://user-images.githubusercontent.com/36489276/206852387-139411e0-b4b9-471b-9b49-dab0459e646a.png)

pilih add record, masukan nama yang akan menjadi domain kita, masukan ip dari webserver, matikan proxy status dan pilih save
![image](https://user-images.githubusercontent.com/36489276/206852586-822fde53-5a2e-4be9-b678-38174c3f7e87.png)

buka webserver nginx, lalu kita masuk ke dalam container nginx
```
docker container exec -i -t nama_container /bin/bash
```
![image](https://user-images.githubusercontent.com/36489276/206852727-7b21c1f6-fa52-4097-8b9a-d3b312b1d85c.png)

masuk ke folder nginx
```
cd /etc/nginx
```
![image](https://user-images.githubusercontent.com/36489276/206852792-d04bca94-bf53-49a7-86c1-b4fb737f6344.png)

buat file reverse proxy baru untuk jenkins
```
nano housy/jenkins.conf
```
![image](https://user-images.githubusercontent.com/36489276/206852814-5aa4be6b-d1c1-4778-b237-832e0c579c7c.png)

buat file konfigurasi, server_name masukan domain kita, location masukan ip publik dari appserver dan port
```
server {
    server_name jenkins.reiya.studentdumbways.my.id;

    location / {
             proxy_pass http://10.116.106.195:8123;
    }
}
```
![image](https://user-images.githubusercontent.com/36489276/206852890-8bf1de1d-6aea-4dfa-859c-34bde9fc0482.png)

cek apakah sudah ada kesalahan syntax
```
nginx -t
```
![image](https://user-images.githubusercontent.com/36489276/206852952-98383dc6-cc40-4bbc-86dd-d4b3d5f972a6.png)

restart nginx
```
service nginx restart
```
![image](https://user-images.githubusercontent.com/36489276/206852968-8929a681-aafe-4da7-a611-a8a4b9e43168.png)

setup reverse proxy berhasil
![image](https://user-images.githubusercontent.com/36489276/206853008-8068bb6c-6957-47f6-a1fa-bd881754c8db.png)

# setup github webhook
pada repository kita, pilih setting
![image](https://user-images.githubusercontent.com/36489276/206853653-bef75800-db98-41b9-ae9a-d4aab901c663.png)

pilih webhooks
![image](https://user-images.githubusercontent.com/36489276/206853662-56f05ef6-4396-4612-beca-6f8aca88d4a4.png)

pilih add webhooks
![image](https://user-images.githubusercontent.com/36489276/206853752-14ca6486-fd55-4e28-aea3-29175c3249e1.png)

pada payload url, masukan domain jenkins kita, tambahkan /github-webhook/ di akhir url, content type pilih aplication/json.
ceklis checkbox just push everything, lalu piilih update webhook
![image](https://user-images.githubusercontent.com/36489276/206853840-054f3b77-132d-4a5f-8657-ecda95af4840.png)

webhook berhasil ditambahkan
![image](https://user-images.githubusercontent.com/36489276/206854016-c6c12bb6-5597-487d-93ea-2c92a1362edf.png)

# membuat job jenkins
pilih create a job
![image](https://user-images.githubusercontent.com/36489276/206851317-0d1d3f34-e0d9-4034-a173-cffb4c663061.png)

sesuaikan nama, pilih pipeline project
![image](https://user-images.githubusercontent.com/36489276/206851265-27464b6a-e550-451d-9981-1f8d11752462.png)

pada bagian build triggers, ceklis github triggers for gitscm polling
![image](https://user-images.githubusercontent.com/36489276/206851355-db543bdb-7923-4134-b95a-8a4d7c731aa3.png)

pilih pipeline from scm, untuk scm pilih git, masukan repository ssh karena kita akan menggunakan private repository (GAGAL)
![image](https://user-images.githubusercontent.com/36489276/206851502-d58ee45a-39c0-4de2-919d-e974a8dee33d.png)

pilih pipeline from scm, untuk scm pilih git, masukan repository https, lalu pilih credential ssh yang sudah kita setting
![image](https://user-images.githubusercontent.com/36489276/206854256-354bc71e-78f2-42eb-9769-9e5c7adfd49d.png)

pilih branch yang akan digunakan, kosongkan bila ingin memilih semua, lalu masukan script path dari jenkinsfile, matikan lightweight checkout
![image](https://user-images.githubusercontent.com/36489276/206854279-14f03c14-715d-4acc-8831-419d9a6d598a.png)

# setup git frontend

buat sebuah jenkinsfile
```
nano Jenkinsfile
```

isikan kurang lebih sebagai berikut
```
def branch = "main"
def nama_repository = "origin"
def dir = "~/housy-frontend/"
def credential = 'housy_jenkins'
def server = 'housy_appserver@103.134.154.8'
def docker_image = 'reiya24/housy-frontend'
def nama_container = 'frontend'

pipeline {
   agent any

    stages {
        stage('pull repository ke github') {
            steps {
                sshagent([credential]){
                    sh
                    """
                    ssh -o StrictHostKeyChecking=no ${server} << EOF
                    echo "Pulling Housy frontend Repository"
                    cd ${dir}
                    docker container stop ${nama_container}
                    docker container rm ${nama_container}
                    git pull ${nama_repository} ${branch}
                    exit
                    EOF
                    """
                }
            }
        }

        stage('build image frontend') {
            steps {
                sshagent([credential]){
                    sh
                    """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    echo "Building Image"
                    cd ${dir}
                    docker build -t ${docker_image}:latest .
                    exit
                    EOF
                    """
                }
            }
        }

        stage('jalankan docker compose') {
            steps {
                sshagent([credential]){
                    sh
                    """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${dir}
                    docker compose -f docker-compose.yaml up -d
                    exit
                    EOF
                    """
                }
            }
        }

        stage('push image ke dockerhub') {
            steps {
                sshagent([credential]){
                    sh """
                    ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${dir}
                    docker image push ${docker_image}:latest
                    exit
                    EOF
                    """
                }
            }
        }
    }
}
```
![image](https://user-images.githubusercontent.com/36489276/206855342-759e0ac6-efd5-4126-a82a-20995320cd09.png)

inisialisasi git menggunakan
```
git init
```
![image](https://user-images.githubusercontent.com/36489276/206854478-a567b109-582b-4c9f-a2ad-dfb2cf9326b3.png)

tambahkan semua file ke staging area
```
git add .
```
![image](https://user-images.githubusercontent.com/36489276/206854546-22557c5e-cd22-4396-acec-64125ef7b459.png)

sebelum commit, konfigurasi email kita
```
git config --global user.email "email"
```
![image](https://user-images.githubusercontent.com/36489276/206854677-55328b36-9cd3-4a93-bff5-43daab44f50a.png)

```
git config --global user.name "nama"
```
![image](https://user-images.githubusercontent.com/36489276/206854730-1d0ee2ce-47f4-4fe0-b14c-047782a6c7a1.png)

buat commit untuk disimpan ke repository git

```
git commit -m "pesan"
```
![image](https://user-images.githubusercontent.com/36489276/206854768-8e8159eb-0899-4925-adb4-2ec9cfe742c7.png)

remote git repository kita ke github
```
git remote add origin url
```
![image](https://user-images.githubusercontent.com/36489276/206854972-c066616f-d3f9-4ac9-bd19-59297434aa99.png)

push ke repository kita ke github menggunakan
```
git push -u origin main
```
![image](https://user-images.githubusercontent.com/36489276/206855258-027cd348-1192-4286-81cf-edbd7ce7e520.png)

jenkins akan otomatis menjalankan script pipeline, tunggu sampai berhasil
![image](https://user-images.githubusercontent.com/36489276/206860541-dc72fda1-55c6-444f-8933-a4ef24b81359.png)



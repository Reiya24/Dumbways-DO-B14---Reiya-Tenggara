# 1. Deploy aplikasi frontend di dalam docker swarm

install docker, clone dan build image terlebih dahulu.
inisalisasi docker swarmnya terlebih dahulu dengan menggunakan perintah
```
docker swarm init
```
atau
```
docker swarm init --advertise-addr ip_address_public_atau_private_untuk_manager
```
![image](https://user-images.githubusercontent.com/36489276/205926621-956b3e3c-a070-42c1-bda4-4111cf3d79eb.png)

lalu deploy appserver menggunakan docker swarm

setelah itu gunakan docker stack untuk mendeploy docker swarm menggunakan file docker compose yang sudah pernah dibuat
```
docker stack deploy --compose-file nama_file_docker_compose nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205971156-e2113e9c-1ae7-4d60-81b0-e65fe49a92ab.png)

lihat semua proses docker swarm yang berjalan dengan menggunakan perintah
```
docker service ls
```
* pada kolom port, docker swarm melakukan port forwarding, artinya port didalam container yang bernilai 3000 (disebelah kanan), di forward ke luar kontainer agar bisa diakses secara publik (disebelah kiri).

setelah itu, kita coba jalankan apakah berhasil dengan mengaksesnya di 

# 2. Hubungkan worker dengan appserver

untuk melihat token untuk di pastekan di worker, kita bisa gunakan perintah
```
docker swarm join-token worker
```
![image](https://user-images.githubusercontent.com/36489276/205978797-13fa8327-6bde-4a28-ae35-1b195e50b3e5.png)

pada virtual machine yang berfungsi sebagai worker, tambahkan user kita untuk dimasukan ke dalam group docker sebelum melakkukan proses join agar tidak terjadi eror seperti ini:
![image](https://user-images.githubusercontent.com/36489276/205981306-2154d3ad-bbcb-4956-819d-f06bf0acd532.png)

gunakan perinatah:
```
sudo usermod -aG docker nama_user
```
![image](https://user-images.githubusercontent.com/36489276/205980953-2d1ace81-a515-4e6d-81b5-a68c1fbb3c30.png)

paste token yang ada di manager
![image](https://user-images.githubusercontent.com/36489276/205981490-1460b7ad-8725-4794-990a-6e8ae11db194.png)

setelah itu, cek apakah service worker dan manager sudah terhubung dengan menggunakan perintah
```
docker node ls
```
![image](https://user-images.githubusercontent.com/36489276/205982082-185ddbf0-9f44-43f7-a749-292eab23f265.png)

# 3 jalankan 2 replika untuk aplikasinya

untuk menambahkan 2 replika, cukup gunakan perintah
```
docker service scale nama_service=jumlah
```
![image](https://user-images.githubusercontent.com/36489276/205984320-f0a0949e-79f0-4b8e-b379-e3f7033145c4.png)

untuk melihat apakah service telah tereplika, gunakan
![image](https://user-images.githubusercontent.com/36489276/205985412-cf5f37d0-a5a9-4f34-83d4-9f0a99e31a05.png)


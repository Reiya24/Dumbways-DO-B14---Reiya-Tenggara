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
![image](https://user-images.githubusercontent.com/36489276/206170532-9a2ddfce-2406-47c6-b028-d50ef81f331a.png)

lalu deploy appserver menggunakan docker swarm

setelah itu gunakan docker stack untuk mendeploy docker swarm menggunakan file docker compose yang sudah pernah dibuat
```
docker stack deploy --compose-file nama_file_docker_compose nama_container
```
![image](https://user-images.githubusercontent.com/36489276/206172266-5dece7ce-1ea4-4d8c-99c8-1545dab545de.png)

lihat semua proses docker swarm yang berjalan dengan menggunakan perintah
```
docker service ls
```
![image](https://user-images.githubusercontent.com/36489276/206175972-36fdeba0-c31e-4ecf-968b-e3707e8b56a4.png)

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
![image](https://user-images.githubusercontent.com/36489276/206175098-bd41ef40-69e6-419c-b17d-4e18e45ca0a4.png)

setelah itu, cek apakah service worker dan manager sudah terhubung dengan menggunakan perintah
```
docker node ls
```
![image](https://user-images.githubusercontent.com/36489276/206179845-980d4d22-bf7a-4fc0-ad70-ac8e3660a675.png)
# 3 jalankan 2 replika untuk aplikasinya

untuk menambahkan 2 replika, cukup gunakan perintah
```
docker service scale nama_service=jumlah
```
![image](https://user-images.githubusercontent.com/36489276/206180346-10366c60-9ecd-4a82-a5f7-b43f2ab9aaa1.png)

untuk melihat apakah service telah tereplika, gunakan
```
docker service ls
```
![image](https://user-images.githubusercontent.com/36489276/206179845-980d4d22-bf7a-4fc0-ad70-ac8e3660a675.png)

4. Web Dapat diakses melalui docker swarm

copy IP public appserver dan worker, setelah itu paste di web browser, tambahkan port 3002 karena container kita berjalaan di port 3002

- Appserver

![image](https://user-images.githubusercontent.com/36489276/206183341-01587f85-caa2-4486-ab6f-47f85da41629.png)

- Worker
![image](https://user-images.githubusercontent.com/36489276/206183466-cfcd1e4f-d070-48fb-9388-eef6172100c8.png)


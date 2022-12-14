# Apa itu docker?

Docker adalah salah satu layanan container manager. Container berfungsi untuk membundling dan mengisolasi semua aplikasi dan depedensi yang diperlukan. Berbeda dengan
virtual machine, Container dapat melakukan itu semua tanpa harus menginstall ulang sistem operasi. Karena container tersebut dijalankan menggunakan sistem operasi dimana
Container manager itu berjalan

Perbandinan perbedaan virtual machine dan container

Virtual machine:

![image](https://user-images.githubusercontent.com/36489276/205448974-01347fca-cd44-4cd5-ba09-05ca68ff544f.png)

Container :

![image](https://user-images.githubusercontent.com/36489276/205448980-8aef60b0-fb29-4d38-8d55-00689bb1622e.png)

# Docker registry

adalah tempat untuk mencari atau menyimpan docker image yang kita buat, dan bisa digunakan di docker daemon manapun selama kita bisa terkoneksi ke docker registry.

kita bisa mencari docker image yang ingin kita unduh di https://hub.docker.com/ 

# Docker image

Di dalam docker image terdapat aplikasi beserta depedensi yang diperlukan sebelum kita bisa menjalankan aplikasi di docker, untuk melihat docker image yang kita punya,
gunakan perintah
```
docker image ls
```
![image](https://user-images.githubusercontent.com/36489276/205455235-c39daac0-38ca-4b62-a34e-597394b6a37f.png)

Untuk mengunduh docker image dari docker registry, gunakan perintah
```
docker image pull nama_image:tag
```
![image](https://user-images.githubusercontent.com/36489276/205456225-a3c4e535-264e-4015-a6fa-3d94d0b86225.png)

tag biasanya digunakan untuk memilih versi mana yang akan di unduh, jika informasi tag tidak diisikan, otomatis docker akan menggunakan tag latest (terbaru)
![image](https://user-images.githubusercontent.com/36489276/205456265-ffcbe290-78b5-42f1-8e5c-11f09e36d9d9.png)

untuk menghapus docker image, gunakan
```
docker image rm nama_image:tag
```
![image](https://user-images.githubusercontent.com/36489276/205456432-a9dd6ad3-bb1b-4fd3-bae9-130086f5def4.png)

# Docker container

Seperti yang sudah dijelaskan diatas, docker container berisi aplikasi dan semua depedensi yang diperlukan untuk menjalankan aplikasi tertentu. 
Satu docker image bisa digunakan untuk membuat banyak docker container, namun bila sudah membuat docker container dari docker image yang dipakai, docker image tersebut tidak bisa dihapus, karena sebenarnya docker container tidak menyalin isi dari docker image, namun hanya menggunakan isinya saja

untuk membuat container, kita bisa gunakan perintah
```
docker container create --name nama_container nama_image:tag
```
![image](https://user-images.githubusercontent.com/36489276/205457967-d6119f3a-a57d-4a76-bd25-d95ab5dd86c7.png)
jika kita membuat docker container yang imagenya belum kita unduh, maka secara otomatis docker akan mengunduh image yang diperlukan

untuk melihat semua container, jalankan
```
docker container ls -a
```
![image](https://user-images.githubusercontent.com/36489276/205457292-aff09e94-e51c-406d-a704-f57faf8dd419.png)

namun bila hanya ingin menggunakan container yang berjalan saja, gunakan perintah:
```
docker container ls
```
![image](https://user-images.githubusercontent.com/36489276/205457342-7669851c-eaa9-4a61-a5ab-d68ceeca77dd.png)


saat membuat container, secara default container tidak akan langsung berjalan, untuk menjalankan container yang sudah dibuat, gunakan perintah
```
docker container start nama_container
```

![image](https://user-images.githubusercontent.com/36489276/205458095-69a39121-19e0-4586-9e68-11965f5a8e80.png)

kita bisa gunakan id container atau gunakan nama containernya untuk menjalankan container

untuk menghentikan container, gunakan perintah:
```
docker container stop nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205458224-162c236c-78b1-44f3-86dd-306a3c05864d.png)

untuk menghapus container (pastikan container di stop terlebih dahulu), gunakan perintah:
```
docker container rm nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205458508-4d6e5041-6039-4073-bcc2-fcbb634273b1.png)

# Container log
untuk melihat kejadian detail dari aplikasi yang berada di container, kita dapat melihatnya di log.

untuk melihat log di container kita, dapat gunakan perintah
```
docker container logs nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205458865-f7087a33-92df-481d-a048-69694ae742b4.png)

untuk melihat log secara realtime, gunakan perintah
```
docker container logs -f nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205458980-4307e172-a164-4f20-ab17-80e4170b724c.png)

# Masuk ke dalam container menggunakan container exec
saat kita membuat container, aplikasi yang terdapat di dalam container hanya bisa diakses dari dalam container itu sendiri, oleh karena itu, kita perlu masuk ke dalam
containernya itu sendiri, untuk masuk ke dalam container, kita bisa gunakan fitur container exec, dimana ia digunakan untuk mengeksekusi kode program yang terdapat di container. jadi fitur exec bukanlah fitur untuk masuk ke dalam container, namun dengan exec kita bisa menjalankan bash shell untuk masuk ke dalam container, karena docker image biasanya dibuat menggunakan linux

untuk masuk ke dalam container, kita bisa mengeksekusi program bash script yang terdapat di dalam container dengan bantuan dari container exec, kita bisa gunakan perintah
```
docker container exec -i -t nama_container /bin/bash
```
![image](https://user-images.githubusercontent.com/36489276/205460002-ae0c75de-f100-43db-93f0-edb327ff31dd.png)

-i berfungsi untuk supaya kita dapat mengirimkan input

-t berfungsi untuk alokasi terminal akses (TTY)

/bin/bash adalah lokasi dari interpreter bash

# Container port
saat menjalankan container, container tersebut terisolasi di dalam docker, berarti komputer utama kita kita tidak bisa mengakses aplikasi yang ada di dalam container secara langung, salah satu cara mengaksesnya adalah menggunakan container exec untuk masuk ke dalam containernya.

Biasanya, sebuah aplikasi berjalan pada port tertentu, namun port yang ada di dalam container tidak bisa kita akses secara langsung di komputer utaman kita, kita perlu melakukan port forwading, yaitu meneruskan sebuah port yang terdapat di komputer utama ke dalam docker container

untuk melakukan port forwading, kita bisa menggunakan perintah berikut ketika sedang membuat container:
```
docker container create --name nama_container --publish posthost:port_container image:tag
```
![image](https://user-images.githubusercontent.com/36489276/205484285-b0ac1f4a-65f3-46cc-9bbb-59f89422a8b9.png)
artinya kita akan mengambil port 8080 di komputer utama kita, lalu diteruskan ke port 80 yang ada di dalam container

jika kita jalankan dan coba di komputer utama kita, maka akan terbuka nginx
![image](https://user-images.githubusercontent.com/36489276/205484838-12213252-f231-4e52-bfed-06423c7ebba3.png)

![image](https://user-images.githubusercontent.com/36489276/205484925-00a96865-01cd-4c60-a87c-2d7c51864f14.png)

# Container environment variable
Dengan mengugnakan environment variable, ktia bisa mengubah-ubah konfigurasi aplikasi, tanpa harus mengubah kode aplikasinya lagi. docker container memiliki
parameter yang bisa kita gunakan untuk mengirim environment variable ke aplikasi yang terdapad di dalam container dengan menggunakan parameter --env atau -e.

contaoh kasus:
kita akan membuat sebuah container dari image mongo db, database mongo db memiliki 2 environment, MONGO_INITDB_ROOT_USERNAME dan MONGO_INITDB_ROOT_USERNAME
![image](https://user-images.githubusercontent.com/36489276/205485867-35fc7041-aaec-41a6-b73c-518365e8a87e.png)

kita bisa menambahakn environment variable dengan menggunakan perintah:
```
docker container create --name nyoba_mongo --env MONGO_INITDB_ROOT_USERNAME=reiya --env MONGO_INITDB_ROOT_PASSWORD=reiya mongo:latest
```
![image](https://user-images.githubusercontent.com/36489276/205485998-916e7336-9fbf-4174-b669-29d9705740d1.png)

# Container stats
untuk melihat penggunaan resource dari tiap continaer yang sedang berjalan, kita bisa gunakan perintah:
```
docker container stats
```
![image](https://user-images.githubusercontent.com/36489276/205487032-4805ccc6-bf74-4b5d-a8bf-981e3672315b.png)

# Docker resource limit
kita bisa mengatur batas penggunaan cpu dan memory container.
dengan cara mengatur limitnya pada saat container itu dubuat.
gunakan perintah --memory untuk mengatur jumlah memori yang digunakan, dan --cpus untuk mengatur jumlah core yang digunakan

contoh kasus:
kita akan membuat docker container dari image nginx dengan melimit penggunaan memorinya hanya bisa 100 mb dan hanya bisa menggunakan 1 core saja
```
docker create --name nyoba_nginx_limit --memory 100m --cpus 1 nginx:latest
```
![image](https://user-images.githubusercontent.com/36489276/205488473-e5a82336-4e6d-4461-8f91-2af01f278521.png)

# Bind mount
untuk mount merupakan kemampuan untuk mounting (shareing) file/folder yang terdapat di komputer utama kita ke dalam folder di dalam container.

contoh kasus:
saya ingin melakukan mounting data di mongo db, direktori tersebut berada di /data/db. saya akan mount di komputer utama saya di folder /home/reiya24/coba_mount
```
docker container create --name nyoba_mongo_bind --mount "type=bind,source=/home/reiya24/coba_mount,destination=/data/db"
```
![image](https://user-images.githubusercontent.com/36489276/205490598-8c17481d-05f1-4888-b62d-3972b08ab192.png)

proses bind berhasil
![image](https://user-images.githubusercontent.com/36489276/205490865-690fe355-2eca-47b0-9927-66aed74b01a9.png)



# Docker Volume
docker volume adalah fitur yang lebih baru dari bind mount, perbadaanya adalah dengan docker volume kita bisa membuat, melihat, dan menghapus volume.
pada bind mounts, data disimpan pada komputer utama kita, sedangkan di volume, data di manage oleh docker.

Secara default semua data pada container itu disimpan di dalam volume.
untuk melihat list volume, gunakan perintah
```
docker volume ls
```
![image](https://user-images.githubusercontent.com/36489276/205509806-ca33ec92-aa69-4506-a775-30a258d1979d.png)
terdapat volume hasil dari pembuatan container

untuk membuat volume, kita bisa gunakan perintah:
```
docker volume create nama_volume
```
![image](https://user-images.githubusercontent.com/36489276/205509859-91eba38b-e6e9-4aad-b834-85d2bb60a544.png)

kita dapat menghapus volume dengan syarat volume tidak digunakan oleh container manapun, dengan menggunakan perintah:
```
docker volume rm nama_volume
```
![image](https://user-images.githubusercontent.com/36489276/205510045-5a69c07c-782a-4168-ac1b-c2d6de833d3e.png)

# Container volume
volume yang sudah dibuat bisa digunakan di container, keuntungan menggunakan volume adalah jika container kita hapus maka data akan tetap aman di volume.
kita dapat menggunakannya dengan perintah
```
docker container create --name nama_volume --mount "type=volume,source=nama_volume,destination=lokasi_container" image:tag
```
![image](https://user-images.githubusercontent.com/36489276/205511007-628bca0a-5a61-4415-b352-be29607d545d.png)

# Docker network
docker memiliki fitur network dimana kita bisa membuat jaringan di dalam docker, dengan itu kita bisa mengkoneksikan container dengan container lain dalam satu network yang sama sehingga bisa saling berkomunikasi.

3 driver network yang populer untuk docker adalah
- bridge : yaitu driver yang digunakan untuk membuat network secara virtual agar container yang terkoneksi di bridge network yang sama bisa saling berkomunikasi
- host : yaitu driver yang digunakan untuk membuat network yang sama pada komputer utama kita, namun fitur ini hanya bisa berjalan di sistem operasi linux
- none : yaitu driver untuk membuat network tidak saling berkomunikasi

untuk membuat network di docker, bisa menggunakan perintah
```
docker network create --driver nama_driver nama_network
```
![image](https://user-images.githubusercontent.com/36489276/205512521-6bb50881-604a-42c4-b564-e9a99fd8fa8a.png)

untuk melihat network, kita dapat menggunakan perintah
```
docker network ls
```
![image](https://user-images.githubusercontent.com/36489276/205512715-70229122-29cf-4cab-b038-3b6c722a9c56.png)

kita bisa menghapus network bila network tersebut tidak digunakan oleh container manapun.
```
docker network rm nama_network
```
![image](https://user-images.githubusercontent.com/36489276/205512827-0eb86cae-f5a5-4484-84c1-4a47ff173786.png)

# Container network
untuk menambahkan container ke network, kita bisa menabahkan perintah --network ketika sedang membuat container baru
```
docker container create --name nama_container --network nama_network image:tag
```
![image](https://user-images.githubusercontent.com/36489276/205513183-6e85a6e6-f4a4-463f-9fc0-e39bb5063c2b.png)

kita bisa menambahkan network ke dalam container yang sudah ada dengan menggunakan perintah
```
docker network connect nama_network nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205513241-b796cf7e-b784-46e8-8fc4-0fdadd6c0bf7.png)

untuk menghapus network yang ada di container, kita bisa gunakan perintah
```
docker network disconnect nama_network nama_contianer
```
![image](https://user-images.githubusercontent.com/36489276/205513992-432ab7de-969a-474d-8cc5-9731098b13a7.png)

# inspect
untuk melihat detail dari image, gunakakn
```
docker image inspect nama_image
```
![image](https://user-images.githubusercontent.com/36489276/205514056-611ca753-d9ba-4c7b-9378-63184b0eaf24.png)

untuk melihat detail dari container, gunakan
```
docker container inspect nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205514096-c44658e0-6895-499b-a0e6-e5a2f3a61b7a.png)

untuk melihat detail dari volume, gunakan
```
docker volume inspect nama_volume
```
![image](https://user-images.githubusercontent.com/36489276/205514192-c0245e14-7fcd-4555-948f-4ca1072f8dda.png)

untuk melihat detail dari network, gunakan
```
docker network inspect nama_network
```
![image](https://user-images.githubusercontent.com/36489276/205514325-c6a4072f-e3cd-4832-b819-16857a60ac9d.png)



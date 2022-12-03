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
docker container start id_container/nama_container
```

![image](https://user-images.githubusercontent.com/36489276/205458095-69a39121-19e0-4586-9e68-11965f5a8e80.png)
kita bisa gunakan id container atau gunakan nama containernya untuk menjalankan container

untuk menghentikan container, gunakan perintah:
```
docker container stop id_container/nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205458224-162c236c-78b1-44f3-86dd-306a3c05864d.png)

untuk menghapus container (pastikan container di stop terlebih dahulu), gunakan perintah:
```
docker container rm id_container/nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205458508-4d6e5041-6039-4073-bcc2-fcbb634273b1.png)

# Container log
untuk melihat kejadian detail dari aplikasi yang berada di container, kita dapat melihatnya di log.

untuk melihat log di container kita, dapat gunakan perintah
```
docker container logs id_container/nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205458865-f7087a33-92df-481d-a048-69694ae742b4.png)

untuk melihat log secara realtime, gunakan perintah
```
docker container logs -f id_container/nama_container
```
![image](https://user-images.githubusercontent.com/36489276/205458980-4307e172-a164-4f20-ab17-80e4170b724c.png)

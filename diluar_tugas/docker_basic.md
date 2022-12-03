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





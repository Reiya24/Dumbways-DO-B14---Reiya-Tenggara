# 1. Devops
Merupakan kepanjangan dari development dan Operation, Dimana devops sendiri berperan untuk menjembatani antara tim Development dan tim Operation. Untuk meningkatkan efisiensi dalam pembuatan sebuah produk aplikasi

#2. 2 Life cycle devops

test ,dimana seorang devops engineer bertugas untuk melakukan sebuah pengetesan kepada sebuah aplikasi sebelum memasuki tahap release

plan
dimana seorang devops engineer bertugas untuk merencatnakan alur


# 3. Instalasi Virtualbox
## Persayaratan
Sebelum Melakukan instalasi Ubuntu server di
virtual machine pada Komputer kita, Dibutuhkan
setidaknya 2 bahan yang perlu kita siapkan.
yaitu Software Virtual Machine dan file ISO Ubuntu Server
itu sendiri.

Virtual Machine berfungsi untuk Menjalankan sebuah
sistem operasi secara virtual, tanpa harus menginstallnya
langsung ke dalam komputer kita.

Ada beberapa perangkat lunak Virtual Machine, 
contohnya yang terkenal yaitu VMware, virtualbox,
dan Qemu.

### Virtual Machine
Pada praktik kali, Saya akan medemonstrasikannya
menggunakan VMware.
Perangkat Lunak tersebut dapat anda 
[unduh disini](https://www.Vmware.com/asean/products/workstation-player/workstation-player-evaluation.html).

### ISO Ubuntu Server

Iso Ubuntu Server adalah sebuah file Installer, yang
akan kita gunakan untuk menginstall ubuntu server itu sendiri
ke dalam virtual machine. File tersebut dapat anda
[unduh disini](https://ubuntu.com/download/server).


## Instalasi ubuntu server di VMware

Pastikan anda telah menginstall VMware dan telah mengunduh
file ISO Ubuntu server di komputer anda

Jika sudah, buka VMware

1. Untuk membuat sebuah Virtual Machine baru, klik “Create a New Virtual Machine”

![1step](https://user-images.githubusercontent.com/36489276/201755234-72e1c942-f9b2-49fd-9314-244eb3fc4c61.png)

2. Pilih “Installer disc image file (iso)”, lalu klik “Browse”, lalu pilih Iso ubuntu yang telah di unduh, Lalu klik next
![image](https://user-images.githubusercontent.com/36489276/201804393-0364b641-3bb3-468f-bee7-5bcdd933d634.png)

3. Silahkan Ubah “Virtual machine name” jika ingin mengubah nama dari virtual machine, Pada contoh kasus kali ini
![image](https://user-images.githubusercontent.com/36489276/201876203-28125f30-51fc-494a-a9aa-15061b7596a2.png)

4.Pilih jumlah disk yang akan digunakan, Pada kasus ini saya akan mengisinya secara default yang direkomendasikan oleh vmware yaitu sebesar 20 giga, biarkan checkbox yang dipilih secara default adalah
![image](https://user-images.githubusercontent.com/36489276/201876427-4bd6b2bd-f8c4-48ce-a97c-97687dd5c25b.png)

5. Klik “Customize Hardware”
![image](https://user-images.githubusercontent.com/36489276/201876586-52667571-f45a-4387-ac1c-216de6536e7c.png)

6. Lalu ubah pengaturan Memory sesuai dengan kebutuhan, Pada kasus ini saya akan memberikan 2 GB
![image](https://user-images.githubusercontent.com/36489276/201876765-f011865a-4fda-4129-a6a0-be1fa521a48f.png)

7. Pada bagian tab processors, Silahkan ubah Number of processor cores sesuai dengan kebutuhan, Pada kasus ini saya hanya akan memberikan 1 core saja.
![image](https://user-images.githubusercontent.com/36489276/201877011-e0bf6434-0a83-4b13-bb61-4388625f99cb.png)

8. Pada tab Network Adapter, Ubah Network connection menjadi Bridged
![image](https://user-images.githubusercontent.com/36489276/201877206-c97b7c56-2180-40aa-8de4-fe7c6e900387.png)

9. Setelah itu klik Close, lalu klik Finish untuk ke tahap selanjutnya.
10. Tunggu beberapa saaat sampai masuk ke bagian instalasi, bila sudah, Pilih “Try or Install Ubuntu server” dengan menggunakan tombol enter
![image](https://user-images.githubusercontent.com/36489276/201877426-899431a8-ed5e-4c95-b46e-140b3bcd9ca0.png)

11. Lalu ubuntu akan melakukan booting untuk memasuki tahap instalasi, Tunggu sampai proses beres.
12. Bila Proses booting sudah selesai maka akan muncul tampilan untuk memilih bahasa, Sesuaikan bahasa yang akan digunakan, lalu tekan enter.

13. Pada bagian ini, Kita pilih saja Continue without updating
![image](https://user-images.githubusercontent.com/36489276/201878045-46a3e76b-05f4-4c78-b816-fc723e31da69.png)

14. Pilih saja menu Done.
![image](https://user-images.githubusercontent.com/36489276/201878225-eb6a548f-2f3a-4d49-a9a0-270fd2f43044.png)

15. Pilih Ubuntu Server (bukan yang versi minimized), Lalu tekan Done.
![image](https://user-images.githubusercontent.com/36489276/201878382-965c4ce6-7b3f-4b07-b06e-1dd046d44796.png)

16. Untuk Mengubah IP dari DHCPv4 menjadi IP static, pilih menu ens33, lalu pilih Edit IPv4, lalu ubah IPv4 method dari automatic menjadi manual. lalu konfigurasi IPv4 agar berubah menjadi static.
![image](https://user-images.githubusercontent.com/36489276/201879129-32f2ec08-cbe6-44e9-b8f8-c721de6ee634.png)
![image](https://user-images.githubusercontent.com/36489276/201879177-54e5dfa9-0df2-4e6e-9d38-66fbbcf61c01.png)
bila berhasil maka tampilan DHCPv4 akan berubah menjadi static
![image](https://user-images.githubusercontent.com/36489276/201879261-a993c26b-d46b-4cbe-9aed-32b4f3f88929.png)

17. Untuk tahap ini kita pilih Done saja
![image](https://user-images.githubusercontent.com/36489276/201879411-6e12b977-a824-4088-a34e-1335ccf578ad.png)

18. PIlih Done lagi
![image](https://user-images.githubusercontent.com/36489276/201879832-54721297-913b-405b-ba4a-b1071aa350a5.png)

19. Pilih free space, lalu Add GPT Partition
![image](https://user-images.githubusercontent.com/36489276/201880002-60890b8b-0527-4cea-b952-6db4afd8ed10.png)

20. Pilih free space, lalu Add GPT Partition
![image](https://user-images.githubusercontent.com/36489276/201880441-b3fe88fa-9e24-4873-82b7-d999082bedee.png)

21. masukan 2G pada menu Size, lalu formatnya pilih Swap, Lalu klik create
![image](https://user-images.githubusercontent.com/36489276/201880530-14e25f70-5b02-4d60-a18b-ae302357d26b.png)

22.pilih free space lagi, lalu Add GPT Partition, lalu klik Create
![image](https://user-images.githubusercontent.com/36489276/201880635-b591525a-efd6-49e0-9bbe-06fde589db7f.png)

23. Setelah partisi swap dan home terbentuk, pilih Done
![image](https://user-images.githubusercontent.com/36489276/201880721-d98c5872-6d50-44ee-8f83-628c245b9179.png)

24. ![image](https://user-images.githubusercontent.com/36489276/201880792-f1e6e14f-ee2e-4901-89a5-46425c8ad51e.png)

25. Seting nama, servername, username, dan password
![image](https://user-images.githubusercontent.com/36489276/201881289-423cf365-6a67-4266-a559-f3b215aeac49.png)

26. Ceklis install OpenSSH server, lalu pilih done
![image](https://user-images.githubusercontent.com/36489276/201881471-29d40f75-f7bf-46f9-8592-c67c16d0a7f5.png)

27. pilih done
![image](https://user-images.githubusercontent.com/36489276/201881700-b56341ad-c39b-4824-af23-0a3d5fd18752.png)

28. Setelah itu akan masuk proses instalasi, tunggu sampai proses instalasi selesai, bila sudah selesai, pilih reboot
![image](https://user-images.githubusercontent.com/36489276/201892871-d6299772-2035-48e9-afaf-d76ed11f884d.png)

29. masukan username dan password
![image](https://user-images.githubusercontent.com/36489276/201893103-2d9027ce-cc35-40fb-90ef-f9bc1997a950.png)

30. ping google.com, atau lakukan update package untuk mengecek koneksi internet sudah tersambung atau belum
![image](https://user-images.githubusercontent.com/36489276/201893388-537dbc09-1dba-4163-941c-3b54f8aeac47.png)





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


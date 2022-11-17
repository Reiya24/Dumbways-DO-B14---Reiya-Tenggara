# 1 Definisi git
merupakan sebuah platform version control system, dimana ia berfungsi untuk memantau dan mencatat semua perubahan dalam sebuat proyek kita, sehingga dengan itu, kita
bisa melihat semua riwayat dalam proyek yang kita kerjakan, kita bisa bisa melihat perbedaannya, serta kita bisa berpindah pindah antar versi

# 2. Rubah IP Address dang mengeceknya dengan menggunakan SSH

untuk mengubah IP address, kita perlu mengubahnya di file konfigurasinya, ia berada di dalam direktori /etc/netplan/50-cloud-init.yaml, kita akses file tersebut
via nano dengan menggunakan hak akses root
```
sudo nano /etc/netplan/50-cloud-init.yaml
```
![image](https://user-images.githubusercontent.com/36489276/202449480-e1557cae-61ca-411c-9c1c-3514d8444301.png)
pada kasus tersebut, IP saya  192.168.100.22/24, saya akan merubahnya ke 192.168.100.44/24
setelah diubah dan di save, kita apply konfigurasi tersebut dengan menggunakan perintah
```
sudo netplan apply
```
![image](https://user-images.githubusercontent.com/36489276/202450244-7abd90d7-3676-4251-a3be-ddf3eb06d2b1.png)

setelah itu kita tes koneksi ubuntu yang berada vmware ke sistem operasi utama kita
```
ssh reiya24@192.168.100.44
```
![image](https://user-images.githubusercontent.com/36489276/202472092-131f0589-5edd-42f5-a9ce-977875bfef0e.png)


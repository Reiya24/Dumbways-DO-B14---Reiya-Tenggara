# 1. Perbedaan antara Shell dan BASH

shell : Sebuah program yang memungkinkan kita untuk mengirimkan sebuah perintah kepada komputer menggunakan text

bash : merupakan salah satu bahasa scripting shell yang berjalan pada sistem operasi berbasis unix (mac os) atau unix like (freebsd, linux) yang berfungsi sebagai penerjemah antara perintah user ke dalam sistem operasi, atau output yang diberikan dari sistem operasi ke user

# 2. membuat bash script untuk update dan upgrade ubuntu server

pertama, kita gunakan nano untuk membuat bash script, jangan lupa bash script menggunakan ektensi berakhiran .sh
```
nano nama_file.sh
```
![image](https://user-images.githubusercontent.com/36489276/203330640-a9c73f4c-14f7-468b-bc25-e35ed5c3063a.png)

untuk baris pertaman kita isikan shebang/hashbang yang berisi path dimana interpreter bash itu berada

catatan: shebang (#!) berfungsi untuk menunjuk path dari shell
contoh : 
- #!/bin/bash maka kita akan menggunakan interpreter dari bash shell
- #!/bin/zsh maka kita akan menggunakan interpreter dari z shell

```
#!/bin/bash
```
![image](https://user-images.githubusercontent.com/36489276/203334801-9de623e2-31d7-4175-8c67-8b35bd3faddc.png)

lalu pada baris kedua, kita masukan perintah untuk mendapatkan repository package index dari ubuntu yaitu
```
sudo apt-get update
```

baris ketiga kita masukan perintah untuk melakuan upgrade sistem, lalu gunakan parameter -y di akhir untuk menginput konfirmasi bernilai y bila muncul output
yang akan ditanyakan
```
sudo apt upgrade -y
```
![image](https://user-images.githubusercontent.com/36489276/203335401-a9d37672-3676-4121-98e9-ca0fe23af394.png)

setelah itu save

kita akan coba menjalankan file tersebut dengan menggunakan perintah
```
./nama_file.sh
```
![image](https://user-images.githubusercontent.com/36489276/203336384-23be7661-92a9-4887-a844-64e1c38b86e1.png)

terkadang kita tidak bisa langsung mengeksekusi scripnya, karena permission di file tersebut tidak mengizinkan kita untuk mengeksekusinya.
solusinya adalah gunakan perintah
```
sudo chmod u+x namafile
```
untuk memberikan akses mengeksekusi pada user yang sedang digunakan
![image](https://user-images.githubusercontent.com/36489276/203350579-e185c54a-0dc9-4347-863b-7e658eb0a7f8.png)




# 3. membuat bash script untuk memberi akses ke port 22, 80 443

kita buat filenya menggunakan nano dengan menggunakan perintah:
```
nano nama_file.sh
```
![image](https://user-images.githubusercontent.com/36489276/203339673-6a60f029-efb1-4980-a383-9b27f2d86990.png)

perintah untuk memberi akses menggunakan port tertentu adalah
```
sudo ufw allow nomor_port
```
karena kasus kali ini saya akan memberi akses ke port 22, 80, 443
maka isikan perintah
```
#!/bin/bash
sudo ufw allow 22, 80, 443
```
![image](https://user-images.githubusercontent.com/36489276/203343814-58c3e64a-c236-425a-891c-efaef2939ec4.png)



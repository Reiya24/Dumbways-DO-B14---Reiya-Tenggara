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

# 3. membuat bash script untuk memberi akses ke port 22, 80 443

kita buat filenya menggunakan nano dengan menggunakan perintah:
```
nano nama_file.sh
```
![image](https://user-images.githubusercontent.com/36489276/203339673-6a60f029-efb1-4980-a383-9b27f2d86990.png)

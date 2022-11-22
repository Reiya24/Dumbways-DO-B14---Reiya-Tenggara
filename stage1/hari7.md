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
saya akan menggunakan menggunakan looping di dalam array, untuk
memenuhi konsep DRY (don't repeat yourself). yaitu pengulangan kode yang
tidak perlu.

kita akan membuat sebuah variable yang berisikan sebuah array, isi dari nilai nilai yang berada di dalam array tersebuat adalah integer yang bernilai nomor nomor port yang akan di allow

```
#!/bin/bash

allowed_port=(22 80 443)
```
![image](https://user-images.githubusercontent.com/36489276/203352967-5cff35bf-0212-4829-9e03-071baeb4d598.png)

setelah itu, kita gunakan for loop
```
for port_number in "${allowed_port[@]}"
do
        sudo ufw allow $port_number
done
```

![image](https://user-images.githubusercontent.com/36489276/203353583-28af09e7-b091-4090-8267-f31f27e1f054.png)

setelah itu, kita gunakan chmod agar scriptnya bisa di eksekusi
```
sudo chmod u+x allow_port.sh
```
![image](https://user-images.githubusercontent.com/36489276/203361573-19a79a8f-776e-4e3d-9b09-676d562b8aed.png)

setelah itu jalankan scriptnya
```
./allow_port.sh
```
![image](https://user-images.githubusercontent.com/36489276/203362714-630dad32-9499-4b20-a10e-17d97c310325.png)

kita cek apakah sudah berhasil, dengan menggunakan perintah
```
sudo ufw status
```
![image](https://user-images.githubusercontent.com/36489276/203363913-ad5b3d86-82af-435d-94a4-5ead7f916d1d.png)

# 4. penggunaan cat, grep, echo sort menggunakan bash script

## 1 cat
pertama kita perlu buat script bashnya terlebih dahulu
```
nano cat_my_ahk_script.sh
```
![image](https://user-images.githubusercontent.com/36489276/203366879-c899e110-d7c1-418a-901f-f0701a84423a.png)

setelah itu, masukan:
```
#!/bin/bash
cat ctrl.ahk
```
![image](https://user-images.githubusercontent.com/36489276/203368209-177d4527-636c-405b-a8f0-c6f1a22f619d.png)

perintah cat berfungsi untuk melihat isi dari file ctrl.ahk

setelah di save, jalankan scriptnya
```
./cat_my_ahk_script.sh
```
![image](https://user-images.githubusercontent.com/36489276/203369609-fe861d9c-6814-4b09-9a25-20ec731b686a.png)

## 2 grep
contoh kasus, saya ingin mencari kata "Administrator" pada file ctrl.ahk

langkah pertama, kita buat file bashnya
```
nano grep_Administrator.sh
```
![image](https://user-images.githubusercontent.com/36489276/203373594-1814dcbb-eff5-42ae-8241-6aa06a7859f9.png)

isikan
```
#!/bin/bash
grep Administrator ctrl.ahk
```
![image](https://user-images.githubusercontent.com/36489276/203375086-ec68a49f-7cec-4a08-b39f-4fbe79c1d0cd.png)

perintah grep berfungsi untuk mencari sebuah kata pada file tertentu, contohnya grep Administrator ctrl.ahk
artinya kita akan mencari kata "Administrator" pada file ctrl.ahk

setelah itu, jalankan file scriptnya
```
./grep_Administrator.sh
```
![image](https://user-images.githubusercontent.com/36489276/203375895-2528b28d-028f-4307-9486-edb13a15a22d.png)

## 3.echo
digunakan untuk mencetak sebuah text, dan kita bisa memasukannya juga ke dalam sebuah file

buat script untuk mencetak sebuah text dan memasukannya ke dalam file dumbways.txt
```
nano dumbways.sh
```
![image](https://user-images.githubusercontent.com/36489276/203379074-82dd3e7e-680c-4b87-9390-ac23e1ef9f44.png)

setelah itu saya akan membuat program while loop, berfungsi untuk mencetak echo "Hello Dumbways!" ke dalam dumbways.txt sebanyak 10 kali
```
 #!/bin/bash
counter=1
while [  $counter -lt 11 ]; do
        echo "$counter Hello Dumbways!" >> dumbways.txt
        let counter=counter+1
done
```
![image](https://user-images.githubusercontent.com/36489276/203382019-4b6e094f-0c1c-480e-ae16-c47cc985916d.png)

setelah itu save dan jalankan
```
./dumbways.sh
```
![image](https://user-images.githubusercontent.com/36489276/203382211-a84253fa-2bfd-4444-abdf-a91d670a3723.png)

setelah itu, kita cat dumbways.txt apakah file script kita berhasil
```
cat dumbways.txt
```
![image](https://user-images.githubusercontent.com/36489276/203382360-4a463f6e-1a91-48b5-82cc-aa685f726aa1.png)

## 4 sort
kita akan mencoba mengurutkan sebuah file yang urutannya berantakan
![image](https://user-images.githubusercontent.com/36489276/203386070-c5fdca27-98d1-40ef-8812-e0abe1d2aa19.png)

kita akan membuat sebuah bash script yang berfungsi untuk mengurutkan file tersebut
```
nano sort_peraturan.sh
```
![image](https://user-images.githubusercontent.com/36489276/203386342-0140e287-45d1-473e-8484-b50fb058f978.png)

```
#!/bin/bash
sort -V belum_di_sort.txt
```
![image](https://user-images.githubusercontent.com/36489276/203387009-4995f632-65c3-437b-96b8-a0b4d704f292.png)

kita akan masukan perintah sort yang berfungsi untuk menyortir, lalu gunakan parameter -V untuk mengurutkannya secara numerik

setelah itu, save dan jalankan
```
./sort_peraturan.sh
```
![image](https://user-images.githubusercontent.com/36489276/203387658-35171a84-c2bf-4f4e-9dfd-dcade24f0f98.png)

## 5 mengganti text Dumbways ke Bootcamp

kita akan mengganti kata Dumbways ke Bootcamp pada file dumbways.txt
![image](https://user-images.githubusercontent.com/36489276/203388580-00061dc3-ecef-4f5a-95cd-eb7604e7d5c0.png)

langkah pertama, buat bash scriptnya
```
nano replace_dumbways_to_bootcamp.sh
```

```
#!/bin/bash
sed -i 's/Dumbways/Bootcamp/g' dumbways.txt
```
![image](https://user-images.githubusercontent.com/36489276/203389295-526ae5f1-c804-4515-a798-5bf4ab5f7cde.png)

kita akan menggunakan perintah sed yang berfungsi untuk melakukan find and replace,

parameter -i berfungsi untuk
![image](https://user-images.githubusercontent.com/36489276/203390096-44469a79-747e-4ee5-a70c-cb831954c25e.png)

lalu s/kata_awal/kata_yang_akan_diganti/g dilanjutkan dengan memasukan nama file yang dituju

setelah itu jalankan filenya, lalu cek hasilnya menggunakan perintah cat dumbways.txt
![image](https://user-images.githubusercontent.com/36489276/203390754-855ec8bd-ef32-4e36-bda3-d8df052b490f.png)




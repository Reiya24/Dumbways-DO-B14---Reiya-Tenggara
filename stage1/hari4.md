# 1 Definisi git
merupakan sebuah platform version control system, dimana ia berfungsi untuk memantau dan mencatat semua perubahan dalam sebuat proyek kita, sehingga dengan itu, kita
bisa melihat semua riwayat dalam proyek yang kita kerjakan, kita bisa bisa melihat perbedaannya, serta kita bisa berpindah pindah antar versi

# 2. Rubah IP Address dan mengeceknya dengan menggunakan SSH

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

# 3 menghubungkan git ke repository
![image](https://user-images.githubusercontent.com/36489276/202478657-e9a21a3a-8589-4131-990e-623ecf72bad4.png)
pertama kita akan buat sebuat repository github
jika berhasil maka akan muncul tampilan seperti ini
![image](https://user-images.githubusercontent.com/36489276/202479078-efcf0b0e-7b81-4c38-a2a4-04fb4c1bd06e.png)

setelah itu, kita perlu mengenerate ssh keygen dengan menggunakakn perintah:
```
ssh-keygen
```
![image](https://user-images.githubusercontent.com/36489276/202483720-7b907afc-a3e0-4d89-a2b1-e28e55df1aec.png)
kita enter saja terus, setelah itu file ssh akan disimpan ke direktori /home/ubuntu/.ssh/id_rsa)

setelah itu, kita perlu masuk ke direktori tersebut, lalu kita copykan isi file id_rsa.pub dengan menggunakan cat
```
cat id_rsa.pub
```
![image](https://user-images.githubusercontent.com/36489276/202484765-6ed6435f-cdc4-4382-9f7b-50dfb3972768.png)

lalu kita masuk ke website github kita, klik profile picture di kanan atas, lalu klik settings, lalu SSH dan GPG keys, lalu klik new SSH keys,
setelah itu masukan kode ssh kita di form keys, untuk title boleh diisi bebas
![image](https://user-images.githubusercontent.com/36489276/202485698-49042623-d744-45bc-b754-3aaff59be428.png)
setelah itu klik add ssh keys

jika ssh keys berhasil, maka akan muncul tampilan kurang lebih seperti dibawah
![image](https://user-images.githubusercontent.com/36489276/202486139-233cfa37-7288-4a66-8b90-23d141d9df55.png)

setelah itu, kita perlu set up konfigurasi git terlebih dahulu.
pertama kita perlu set up nama git kita menggunakan perintah:
```
git config --global user.name "Reiya Tenggara"
```
![image](https://user-images.githubusercontent.com/36489276/202488237-a28a38ef-9e7c-4fda-80dc-22238ac83685.png)
serta kita perlu set up email git kita menggunakan perintah:
```
git config --global user.email "reiya2307@gmail.com"
```
![image](https://user-images.githubusercontent.com/36489276/202489446-eb038746-a254-41ab-acc3-607a9c01efdf.png)

setelah itu, kita tes koneksi git kita ke github dengan menggunakan perintah:
```
ssh -T git@github.com
```
![image](https://user-images.githubusercontent.com/36489276/202489737-63be98f3-51c9-4abc-b796-e1d15da8a5d3.png)

setelah itu, kita remote git menggunakan command
```
git remote add origin git@github.com:Reiya24/test_clone.git
```
![image](https://user-images.githubusercontent.com/36489276/202507632-26abceb2-086a-4488-802c-6e6defece76b.png)

jika ingin mengupload semua perubahan git kit ke dalam github, kita menggunakan command:
```
git push --set-upstream origin master
```
![image](https://user-images.githubusercontent.com/36489276/202509307-ef44a28a-8426-4a51-a076-ea14e4f01b58.png)

file berhasil di upload
![image](https://user-images.githubusercontent.com/36489276/202509475-f7b8495a-78c1-47b6-b0f9-52ee55b21444.png)

# 4 membuat 3 buah branch

untuk membuat sebuah branch dalam git, kita tinggal mengetikan perintah
```
git branch nama_branch_baru
```
![image](https://user-images.githubusercontent.com/36489276/202513777-1506e574-ae98-4bdd-920e-ea7f71601067.png)

untuk melihat semua branch cukup ketikan
```
git branch
```
![image](https://user-images.githubusercontent.com/36489276/202514242-3c98cdca-6965-4904-800a-d3c953ca34ac.png)








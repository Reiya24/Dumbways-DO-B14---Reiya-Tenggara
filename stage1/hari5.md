# 1 Definisi CI/CD

CI/CD adalah sebuah konsep untuk mengautomatisasi agar proses development life cycle dapat berjalan dengan secepat mungkin dan se efisien mungkin
![image](https://user-images.githubusercontent.com/36489276/202966151-e58b7d46-b0f3-4b1b-bb1e-343300fd9135.png)

A. Continuous Integration
merupakan sebuah proses untuk mangautomatisasi pada proses development, yaitu pada proses code > build > test.
Contoh kasusnya. saya sedang mengerjakan sebuah aplikasi Android dan ingin mengetesnya, dengan adanya CI, kita hanya perlu mengirimnya ke service tertentu, lalu
di service inilah program kita akan secara di build secara otomatis, lalu akan dilakukan proses testing secara otomatis dan berulang - ulang, bila terdeteksi sebuah bug, maka service tersebut akan memberi tahu kita untuk memperbaikinya, namun bila lolos test, maka secara otomatis program kita akan masuk ke taham selanjutnya

![image](https://user-images.githubusercontent.com/36489276/202970159-c1488975-2cc5-4261-a3bf-dd6bf24c42ed.png)

B. Setelah proses CI selesai, maka akan masuk ke tahap Continuous Deployment, yaitu dimana bila program sudah lolos testing, maka secara otomatis program tersebutakan terdeploy secara otomatis

C. Continuous Delivery, merupakan proses yang lebih tradisional dari Continuous Development, dimana program yang sudah lolos pada tahap CI akan disimpan ke dalam suatu Repository, sehingga program tersebut bisa kita deploy secara manual atau 
bisa dilakukan pengujian ulang terlebih dahulu secara manual

# 2 melakukan fork pada repository dumbfilix

Kita masuk dulu ke repository dumbflix

https://github.com/dumbwaysdev/dumbflix-frontend


lalu klik tombol fork yang ada di kanan atas
![image](https://user-images.githubusercontent.com/36489276/203003715-72450cf6-c828-4c63-a162-382acdb37545.png)

setelah itu klik create fork
![image](https://user-images.githubusercontent.com/36489276/203006190-d53b7113-cfaf-4d27-9186-3a8c59843507.png)

setelah itu buka halaman dashboard pada cloudflare
https://dash.cloudflare.com/
pastikan anda sudah memiliki akun clouflare terlebih dahulu, jika belum, silahkan mendaftar lalu login menggunakan akun yang baru dibuat
bila sudah, pilih menu pages yang berada di sebelah kiri
![image](https://user-images.githubusercontent.com/36489276/203007352-d2c7b1d4-95e9-4368-ac46-2b7ad238eef1.png)

setelah itu klik create a project
![image](https://user-images.githubusercontent.com/36489276/203007623-54a12e7d-72cf-449c-bf0f-77f256efc6fa.png)

setelah itu klik connect to git
![image](https://user-images.githubusercontent.com/36489276/203009540-58d60ace-04f5-4240-9353-4864f3464e2f.png)

pilih connect github
![image](https://user-images.githubusercontent.com/36489276/203013341-3a09acbf-e664-4552-b0a6-df20aab521fe.png)

klik checkbox all repositories agar cloudflare dapat melihat semua repository
atau only select repository agar cloudflare hanya bisa mengakses repository tertentu saja, pada kasus kali ini saya angkan mengklik checkbox all repositories
![image](https://user-images.githubusercontent.com/36489276/203013957-6fd1ad10-fc5a-4525-811c-bfd4d77c841c.png)

setelah itu klik install & authorize

pilih repository yang akan di deploy lalu klik begin setup
![image](https://user-images.githubusercontent.com/36489276/203018526-d76eb822-a06c-4534-94ea-b2b3d577314f.png)

karena kita akan mendeploy aplikasi yang menggunakan framework react, maka pada bagian framework preset, kita pilih create react app,
lalu pilih save and deploy
![image](https://user-images.githubusercontent.com/36489276/203020162-5dbb7153-a4b6-4948-91de-beaa5d6e1322.png)




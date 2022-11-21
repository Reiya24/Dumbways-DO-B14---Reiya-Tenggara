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

pilih repository yang akan di deploy lalu click begin setup
![image](https://user-images.githubusercontent.com/36489276/203022172-6b2eca5a-07bb-4c75-ac58-36bda810e291.png)

karena kita akan mendeploy aplikasi yang menggunakan framewrok react, pada bagian framework preset kita pilih create react app
lalu pilih save and deploy

![image](https://user-images.githubusercontent.com/36489276/203022390-03fff030-a0cc-48d0-bee8-299d425ed361.png)

tunggu proses deployment selesai
![image](https://user-images.githubusercontent.com/36489276/203022822-84dddbbb-5102-4566-9fb0-932dee505098.png)

bila sudah sukses, klik continue to project

klik link yang diberi tanda
![image](https://user-images.githubusercontent.com/36489276/203024455-34d52f8a-535b-4498-83f4-ac12ef38bbd5.png)

proses deploy berhasil bila muncul homepage dari dumbflix
![image](https://user-images.githubusercontent.com/36489276/203024738-622a5a89-d4de-41a4-8ff6-9f616fa9c6c5.png)

saya akan mencoba membuat commit baru dengan merubah judul dari homepage dumbflix, filenya berada di dumbflix-frontend/public/index.html.

klik icon edit
![image](https://user-images.githubusercontent.com/36489276/203026106-a654bbad-a5d0-458e-882c-034e2902a8da.png

saya akan ubah titlenya menjadi nama saya, setelah itu klik commit changes
![image](https://user-images.githubusercontent.com/36489276/203028398-21ae7e8d-6ec5-4a63-b8a4-46f818854067.png)

setelah itu cloudflare akan mendeteksi bila ada commit baru, dan cloudfare akan dengan sendirinya mendeploy ulang aplikasi tersebut
![image](https://user-images.githubusercontent.com/36489276/203028721-1fc49713-3014-4c4e-beae-7fd7fa6dfe54.png)

setelah deploy ulang berhasil, kita refresh lagi websitenya

![image](https://user-images.githubusercontent.com/36489276/203028877-6ee3bcee-95ed-4a28-833b-226c1406e0e7.png)

jika judul sudah berubah, maka proses deploy sudah berhasil






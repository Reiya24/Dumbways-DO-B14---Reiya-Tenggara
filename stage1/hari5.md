# 1 Definisi CI/CD

Secara keseluruhan CI/CD adalah sebuah konsep untuk mengautomatisasi agar proses development life cycle dapat berjalan dengan secepat mungkin dan se efisien mungkin
![image](https://user-images.githubusercontent.com/36489276/202966151-e58b7d46-b0f3-4b1b-bb1e-343300fd9135.png)

A. Continuous Integration
merupakan sebuah proses untuk mangautomatisasi pada proses development, yaitu pada proses code > build > test.
Contoh kasusnya. saya sedang mengerjakan sebuah aplikasi Android dan ingin mengetesnya, dengan adanya CI, kita hanya perlu mengirimnya ke service tertentu, lalu
di service inilah program kita akan secara di build secara otomatis, lalu akan dilakukan proses testing secara otomatis dan berulang - ulang, bila terdeteksi sebuah bug, maka service tersebut akan memberi tahu kita untuk memperbaikinya, namun bila lolos test, maka secara otomatis program kita akan masuk ke taham selanjutnya

![image](https://user-images.githubusercontent.com/36489276/202970159-c1488975-2cc5-4261-a3bf-dd6bf24c42ed.png)
B. Setelah proses CI selesai, maka akan masuk ke tahap Continuous Deployment, yaitu dimana bila program sudah lolos testing, maka secara otomatis program tersebut
akan terdeploy secara otomatis

C. Continuous Delivery, merupakan proses yang lebih tradisional dari Continuous Development, dimana program yang sudah lolos pada tahap CI akan disimpan ke dalam suatu Repository, sehingga program tersebut bisa kita deploy secara manual atau 
bisa dilakukan pengujian terlebih dahulu secara manual

# 2 melakukan fork pada repository dumbfilix

Kita masuk dulu ke repository dumbflix

https://github.com/dumbwaysdev/dumbflix-frontend
